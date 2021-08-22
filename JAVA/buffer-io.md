# Buffer I/O
```
210819 TIL #17 BufferedReader / BufferedWriter
사용 언어 : JAVA
```
## ✔️ BufferedReader / BufferedWriter란?
버퍼를 이용해 사용자의 입력을 읽고 쓰는 함수이다.

버퍼를 사용하기 때문에 이 함수를 이용하면 입출력의 효율이 비교할 수 없을 정도로 좋아진다.

### ❓ Scanner 와 BufferedReader 의 차이
 **Scanner**는 스페이스와 개행문자를 경계로 입력 값을 인식하기 때문에 가공할 필요가 없어 **편리하지만 속도가 느리다**. 특히 BOJ와 같은 알고리즘 문제를 풀 때 시간 초과 에러를 많이 보인다. 
 
 반대로 **BufferedReader** 는 개행문자만 경계로 인식하고 받은 데이터가 String으로 고정되기 때문에 데이터를 따로 가공해야 해서 **번거롭지만 버퍼를 사용하기에 입력 속도에서 확연한 차이**를 보인다.

 ![image](https://user-images.githubusercontent.com/78305431/129995440-5871107e-3e7f-4eda-9731-29d71ef8a3cf.png)
'버퍼를 거쳐가는데 왜 더 빠른거지 더 느려야 정상 아니냐!' 라고 생각할 수 있다. 그러나 데이터 입출력은 원래 느리다. 그러므로 **한번에 버퍼에 모아 이동시키는 것이 훨씬 빠르고 효율적**이다.
```
버퍼(buffer) : 데이터를 한 곳에서 다른 곳으로 전송하는 동안 일시적으로 그 데이터를 보관하는 임시 메모리 영역
```

실제로 입력 방식에 대한 속도 차이를 나타낸 표를 보면 극명히 차이가 드러난다.
![image](https://user-images.githubusercontent.com/78305431/129995516-20b0e73b-f0b7-4b0a-871c-8d218795d54c.png)

***

## ✔️ BufferedReader 
입력 스트림에서 문자를 읽는 함수

문자나 배열, 라인을 효과적으로 읽기 위해 문자를 버퍼에 저장하고 읽는 방법을 취한다. 버퍼 사이즈는 사용자가 지정할 수 있지만 따로 지정을 하지 않는 경우 디폴트 사이즈가 사용된다.

## ✔️ BufferedReader 사용법
BufferedReader의 readLine()은 데이터를 라인 단위로 읽을 수 있게 해준다.

키보드 입력 -> inputstream ->inputstreamreader ->bufferedreader -> br.readLIne() 

순으로 입력값을 가져온다.

[한 줄 데이터 읽기]
```java
import java.io.*;

class BufferReader {
	public static void main(String[] args) {
    	try { //예외처리 필수 또는 throwsIOExeption 
        	
            // 1) 콘솔에서 입력 받는 경우
            BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
            
            //return 값이 String이므로 형변환
            int num = Integer.parseInt(br.readLine());
            br.close(); //입출력이 끝난 후 close
            
            // 2) 파일에서 입력 받는 경우
            FileReader fr = new FileReader("BufferReaderFile.java");
            BufferedReader br_file = new BufferedReader(fr);
            
            //파일의 한 줄씩 읽어서 출력한다.
         	String line = "";
            for (int i = 1; (line = br_file.readLine()) != null; i++) {
            	System.out.println(line);
            }
        } catch (IOException e{
        	e.printStackTrace();
            System.out.println(e.getMessage());
         	}
     }
}
```

[공백 단위로 데이터 읽기]
StringTokenizer의 nextToken 함수를 이용하거나 String 클래스의 split 함수를 이용하는 방법이 있다.
```java
/*
백준같은 코딩 테스트 문제에서 주로 입력으로 나오는
ex )
5
2 3 2 1 5
와 같은 입력을 받는 예제 
*/
BufferedReader br = new BufferedReader(new InputStreamReader(System.in));
int N = Integer.parseInt(br.readLine);

// 1) 디폴트 구분자가 공백
StringTokenizer st = new StringTokenizer(br.readLine());

// 2) 다른 구분자를 원하는 경우
StringTokenizer st = new StringTokenizer("자르고자 하는 문자열", "구분자");

for(int i = 0; i < N; i++) {
	p[i] = Integer.parseInt(st.nextToken());
}
```
## ✔️ BufferedReader 메소드
<table style="border-collapse: collapse; width: 100%; height: 200px;" border="1" data-ke-align="alignLeft" data-ke-style="style15">
<tbody>
<tr style="height: 20px;">
<td style="width: 25%; text-align: center; height: 20px;">메소드 이름</td>
<td style="width: 25%; text-align: center; height: 20px;">반환형</td>
<td style="width: 50%; text-align: center; height: 20px;">설명</td>
</tr>
<tr style="height: 20px;">
<td style="width: 25%; text-align: center; height: 20px;">close()</td>
<td style="width: 25%; text-align: center; height: 20px;">void</td>
<td style="width: 50%; text-align: center; height: 20px;">입력 스트림을 닫고 사용하던 자원들을 푼다.</td>
</tr>
<tr style="height: 20px;">
<td style="width: 25%; text-align: center; height: 20px;">mark(int readAheadLimit)</td>
<td style="width: 25%; text-align: center; height: 20px;">void</td>
<td style="width: 50%; text-align: center; height: 20px;">스트림의 현재 위치를 마킹한다.</td>
</tr>
<tr style="height: 20px;">
<td style="width: 25%; text-align: center; height: 20px;">markSupported()</td>
<td style="width: 25%; text-align: center; height: 20px;">boolean</td>
<td style="width: 50%; text-align: center; height: 20px;">스트림이 mark 기능을 지원하는지 알려준다.</td>
</tr>
<tr style="height: 20px;">
<td style="width: 25%; text-align: center; height: 20px;">read()</td>
<td style="width: 25%; text-align: center; height: 20px;">int</td>
<td style="width: 50%; text-align: center; height: 20px;">한 글자만 읽어 정수형으로 반환한다. String으로 읽기 때문에 3을 입력해도 '3' 으로 읽기 때문에 (int)'3' = 51을 반환한다.</td>
</tr>
<tr style="height: 20px;">
<td style="width: 25%; text-align: center; height: 20px;">read(char[] cbuf, int offset, int length)</td>
<td style="width: 25%; text-align: center; height: 20px;">int</td>
<td style="width: 50%; text-align: center; height: 20px;">cbuf의 offset 위치부터 length길이만큼 문자를 스트림으로부터 읽어온다.</td>
</tr>
<tr style="height: 20px;">
<td style="width: 25%; text-align: center; height: 20px;">readLine()</td>
<td style="width: 25%; text-align: center; height: 20px;">String</td>
<td style="width: 50%; text-align: center; height: 20px;">한 줄을 읽어 String으로 반환한다.</td>
</tr>
<tr style="height: 20px;">
<td style="width: 25%; text-align: center; height: 20px;">ready()</td>
<td style="width: 25%; text-align: center; height: 20px;">boolean</td>
<td style="width: 50%; text-align: center; height: 20px;">입력 스트림이 사용할 준비가 되어있는지 확인해준다.</td>
</tr>
<tr style="height: 20px;">
<td style="width: 25%; text-align: center; height: 20px;">reset()</td>
<td style="width: 25%; text-align: center; height: 20px;">void</td>
<td style="width: 50%; text-align: center; height: 20px;">마킹이 있으면 그 위치부터 다시 시작, 그렇지 않으면 처음부터 다시 시작한다.</td>
</tr>
<tr style="height: 20px;">
<td style="width: 25%; text-align: center; height: 20px;">skip(long n)</td>
<td style="width: 25%; text-align: center; height: 20px;">long</td>
<td style="width: 50%; text-align: center; height: 20px;">n개의 문자를 건너띈다.</td>
</tr>
</tbody>
</table>

***

## ✔️ BufferedWriter
System.out.println()과 동일하게 사용 가능한 함수이다. 버퍼를 이용하기 때문에 **성능면에서 훨씬 좋고 많은 양의 출력이 필요할 때**에는 마찬가지로 BufferdeWriter를 사용하는 것이 좋다.

System.out.println()처럼 함수가 문자열 출력과 개행을 동시에 해주지 않기 때문에 개행을 하려면 write에 "\n"을 넣어주거나 newLine함수를 사용해야 한다.
```java
import java.io.*;

class BufferedWriterExample {
	public static void main(String[] args) throws IOExeption {
        // 1) 콘솔창 출력
        BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(System.out));

        // 2) 파일 출력
    	BufferedWriter bw = new BufferedWriter(new FileWriter("bufferedWriter.txt"));
        
        bw.write("hello");
        bw.newLine(); //개행
        bw.write("I am writing\n"); //개행과 함께 출력
        bw.flush(); //남아있는 데이터를 모두 출력
        bw.close(); //스트림을 닫아줌
        }
}
```

## ✔️ 주의할 점
- 버퍼 기반이기 때문에 출력하려고 넣은 값이 **버퍼 사이즈보다 작으면 flush()** 해주어야 한다.

- 버퍼를 이용하며 다 사용하고 나서 **버퍼를 비워줘야 한다.**  flush() 함수를 통해서 남아 있는 데이터를 모두 출력 해 없애주고 스트림을 닫아준다.

- **인자로 String 형태를 넣어야 한다**. 만약 int 값을 그냥 write()로 넘겨준다면 이상한 문자가 출력된다. write() 함수가 여러가지로 오버로딩이 되어있어 int형을 인자로 받을 수는 있지만 그것은 정수를 입력받는 용도가 아니라, char를 int로 입력받는 것이기 떄문에 최종 출력값에는 아스키코드에 따른 캐릭터형 값이 나온다.

## ✔️ BufferedWriter 메소드
<table style="border-collapse: collapse; width: 100%; height: 140px;" border="1" data-ke-align="alignLeft" data-ke-style="style15">
<tbody>
<tr style="height: 20px;">
<td style="width: 33.3333%; text-align: center; height: 20px;">메소드 이름</td>
<td style="width: 33.3333%; text-align: center; height: 20px;">반환형</td>
<td style="width: 33.3333%; text-align: center; height: 20px;">메소드 설명</td>
</tr>
<tr style="height: 20px;">
<td style="width: 33.3333%; text-align: center; height: 20px;">close()</td>
<td style="width: 33.3333%; text-align: center; height: 20px;">void</td>
<td style="width: 33.3333%; text-align: center; height: 20px;">스트림을 닫는다. 닫기 전에 flushing이 필요하다.</td>
</tr>
<tr style="height: 20px;">
<td style="width: 33.3333%; text-align: center; height: 20px;">flush()</td>
<td style="width: 33.3333%; text-align: center; height: 20px;">void</td>
<td style="width: 33.3333%; text-align: center; height: 20px;">스트림을 비운다.</td>
</tr>
<tr style="height: 20px;">
<td style="width: 33.3333%; text-align: center; height: 20px;">newLine()</td>
<td style="width: 33.3333%; text-align: center; height: 20px;">void</td>
<td style="width: 33.3333%; text-align: center; height: 20px;">개행 문자 역할을 한다.</td>
</tr>
<tr style="height: 20px;">
<td style="width: 33.3333%; text-align: center; height: 20px;">write(char[] cbuf, int offset, int length)</td>
<td style="width: 33.3333%; text-align: center; height: 20px;">void</td>
<td style="width: 33.3333%; text-align: center; height: 20px;">버퍼 offset의 위치부터 length 크기만큼 write를 쓴다.</td>
</tr>
<tr style="height: 20px;">
<td style="width: 33.3333%; text-align: center; height: 20px;">write(int c)</td>
<td style="width: 33.3333%; text-align: center; height: 20px;">void</td>
<td style="width: 33.3333%; text-align: center; height: 20px;">한 글자를 쓴다.</td>
</tr>
<tr style="height: 20px;">
<td style="width: 33.3333%; text-align: center; height: 20px;">write(String s, int offset, int length)</td>
<td style="width: 33.3333%; text-align: center; height: 20px;">void</td>
<td style="width: 33.3333%; text-align: center; height: 20px;">문자열에서 offset부터 length 크기만큼 write를 쓴다.</td>
</tr>
</tbody>
</table>

***
참고 
https://jhnyang.tistory.com/92

https://m.blog.naver.com/PostView.naver?isHttpsRedirect=true&blogId=chltmddus23&logNo=221696297647 