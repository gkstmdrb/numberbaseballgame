# numberbaseballgame
# 숫자로 하는 야구 게임
### 규칙
<br>
배열방 3개에 1~9까지의 숫자가 겹치지 않도록 난수를 발생시킨다. <br>
사용자는 1~9사이에 3개의 숫자와 자리배치를 맞춰야한다. <br>
입력한 자리와 숫자 모두 맞았다면, strike <br>
입력한 숫자만 맞았다면 ball의 값을 1 증가시킨다. <br>
3개의 숫자를 모두 입력했다면 strike와 ball의 개수를 출력한다. <br>
이렇게 사용자는 strike와 ball이 나오는 것을 보며 숫자의 배치를 맞춰나가는 게임이다. <br>
최대 시도 횟수는 11회이며, <br>
3번 이하면 "참 잘했어요!" <br>
5번 이하면 "잘했어요!" <br>
9번 이하면 "보통이네요!" <br>
10번 이상이면 "분발하세요!" 를 출력한다. <br>
<br><br><br>

## 설계
<br>
컴퓨터가 랜덤으로 선택하는 숫자 3개를 넣을 x, y, z를 생성하고, 랜덤값을 넣는다. <br>
이 값을 토대로 사용자가 입력한 숫자와 자리배치를 비교할 com 배열방을 생성한다. <br><br>

게임 시도 횟수를 세는 count방과 숫자 매칭에 따른 결과를 나타낼 strike, ball 방을 생성한다. <br><br>

사용자가 입력한 값을 저장 할 user 방과 그 입력한 값을 넣을 usr 배열방을 생성한다. <br>
사용자가 입력한 3개의 숫자를 usr 배열방에 넣는다. <br><br>

입력한 값이 중복이 되지 않고 1-9까지 범위에서만 입력할 수 있도록 if문을 사용한다. <br>
모든 숫자가 1-9사이, 같은 숫자가 없는 경우에만 반복문을 빠져나온다. <br><br>

usr, com 두 개의 배열이 각각 완전히 일치할 경우에만 strike 처리를 한다. <br>
usr, com 두 개의 배열의 데이터 위치가 다른 경우에만 ball 처리를 한다. <br><br>

시도 횟수를 if문으로 판별하여 위 텍스트를 출력한다.<br><br><br>

## 구현
``` java
import java.util.*;
import java.io.*;

	public class baseball {
		public static int playGame() throws IOException  {
			//컴퓨터가 3개의 난수를 발생시키는 메소드
			
			int x, y, z; 
			//컴퓨터가 선택하는 3개 숫자
			Random r = new Random(); 
			//난수발생 Random()메소드로 객체변수 r 생성
			
			x = Math.abs(r.nextInt() % 9) + 1; 
			// 1~9 사이의 난수 발생
			
			do {
				y = Math.abs(r.nextInt() % 9) + 1;
			} while (y==x); 
			// 만일 난수 y가 x와 같은 수일 때 다시 한 번 난수 발생 반복
			do {
				z = Math.abs(r.nextInt() % 9) + 1;
			} while ((z==x)||(z==y)); // 만일 난수 y가 x 혹은 y와 같은 수일 때 다시 한 번 난수 발생 반복
			
			System.out.println(x +", "+ y +", "+ z); //컴퓨터가 발생시킨 난수 확인(게임 시 비공개)
		
			return playGame(x, y, z);
		}
			
	public static int playGame (int x, int y, int z) throws IOException {
		// 인수 3개가 주어지는 메소드
			
			int count; //게임을 시도하는 횟수
			int strike, ball; // 숫자 매칭에 따른 결과
				
			int[] usr = new int[3]; // 사용자가 입력하는 숫자 3개를 저장하는 배열
			int[] com = {x, y, z}; // 컴퓨터가 선택한 숫자 3개를 저장하는 배열
				
			System.out.println("숫자 야구 게임");
				
			count = 0;
			
			do {
			
			count++;
			do {
				System.out.println("\n카운트: " + count);
					
				BufferedReader in = new BufferedReader(new InputStreamReader(System.in));
				// 콘솔 화면에서 사용자가 입력하는 데이터를 받아들이는 BufferedReader() 메소드의 객체변수 in 생성
				String user; //객체변수 in에 들어있는 데이터내용을 문자형데이터로 저장할 변수생성
					
				System.out.print("1번째 숫자: ");
				user = in.readLine(); 
				// 사용자가 입력하는 데이터를 변수 user 에 저장
        
				usr[0] = new Integer(user).intValue(); 
				// 변수 user에 저장된 데이터를 정수형으로 변환시켜 배열 0번칸에 저장
				// 반복
        
				System.out.print("2번째 숫자: ");
				user = in.readLine(); 
				usr[1] = new Integer(user).intValue(); 
					
				System.out.print("3번째 숫자: ");
				user = in.readLine();  
				usr[2] = new Integer(user).intValue(); 
			
				if ((usr[0]==0)||(usr[1]==0)||(usr[2]==0)) {
					System.out.println("0은 입력하지 마세요. 다시 입력해주세요.");
				} else if((usr[0]>9)||(usr[1]>9)||(usr[2]>9)){
					System.out.println("1부터 9까지의 숫자 중 하나를 입력해주세요. 다시 입력해주세요.");
				} else if((usr[0]==usr[1])||(usr[1]==usr[2])||(usr[0]==usr[2])){
					System.out.println("모두 다른 숫자를 입력해주세요. 다시 입력해주세요.");
				}
			} while((usr[0]==0)||(usr[1]==0)||(usr[2]==0)||
					(usr[0]>9)||(usr[1]>9)||(usr[2]>9)||
					(usr[0]==usr[1])||(usr[1]==usr[2])||(usr[0]==usr[2]));
					//모든 숫자가 1~9사이, 같은 숫자가 없는 경우에만 반복문을 빠져나옴
				
			strike = ball = 0;
						
			if (usr[0]==com[0]) strike++;
			if (usr[1]==com[1]) strike++;
			if (usr[2]==com[2]) strike++; 
			//usr, com 두 개의 배열이 각각 완전히 일치할 경우에만 strike 처리
						
			if(usr[0]==com[1]) ball++;
			if(usr[0]==com[2]) ball++;
			if(usr[1]==com[0]) ball++;
			if(usr[1]==com[2]) ball++;
			if(usr[2]==com[0]) ball++;
			if(usr[2]==com[1]) ball++; 
			//usr, com 두 개의 배열의 데이터 위치가 다른 경우에만 ball 처리
					
			System.out.println("Strike: "+ strike +" Ball: "+ ball);
		} while ( (strike<3)&&(count<11) ); 	//strike<3(게임미완성),count<11(시도횟수 10번까지)일 때 반복
                                           //strike=3 이거나 count=11(시도횟수 11번째)가 되면 종료
		return count;
	}
			
	public static void main(String[] args) throws IOException {
			
		int result; //게임 결과값을 위한 변수 생성
			
		if (args.length==3) { 
			int x = Integer.valueOf(args[0]).intValue();
			int y = Integer.valueOf(args[1]).intValue();
			int z = Integer.valueOf(args[2]).intValue();
			// 게임실행 주어진 3개인 경우, 각각 정수형으로 형변환을 통해 x,y,z 에 저장
      
			result = playGame(x, y, z);
		} else { 				       // 난수발생시키는 경우 즉, playGame()에 해당
			result = playGame(); // return 값 즉, 시도횟수(count)를 결과값으로 반환하여 result에 저장
		}
			
		System.out.println();
		if (result<=2) {
			System.out.println("참 잘했어요!");   //시도횟수가 2번 이하
		} else if (result<=5){
			System.out.println("잘했어요!"); 		 //시도횟수가 3번부터 5번 이하
		} else if (result<=9){
			System.out.println("보통이네요!"); 		 //시도횟수가 6번~9번
		} else {
			System.out.println("분발하세요!");		 //시도횟수가 10번
		}
	}
}
```
