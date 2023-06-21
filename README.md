# numberbaseballgame
# 숫자로 하는 야구 게임
### 규칙
<br>
배열방 3개에 1~9까지의 숫자가 겹치지 않도록 난수를 발생시킨다. <br>
사용자는 1~9사이에 3개의 숫자와 자리배치를 맞춰야한다. <br><br>

입력한 자리와 숫자 모두 맞았다면, strike <br>
입력한 숫자만 맞았다면 ball의 값을 1 증가시킨다. <br><br>

3개의 숫자를 모두 입력했다면 strike와 ball의 개수를 출력한다. <br><br>

이렇게 사용자는 strike와 ball이 나오는 것을 보며 숫자의 배치를 맞춰나가는 게임이다. <br><br>

최대 시도 횟수는 11회이며, <br>
3번 이하면 "참 잘했어요!" <br>
5번 이하면 "잘했어요!" <br>
9번 이하면 "보통이네요!" <br>
10번 이상이면 "분발하세요!" 를 출력한다. <br><br><br>
## 실행 화면
정답: 2 5 1 <br><br>
![image](https://github.com/gkstmdrb/numberbaseballgame/assets/114748816/e6741407-4c00-4459-a23e-7a74efe0e066) <br>
1: 입력 값은 1 2 3 이므로 1과 2를 포함하나 자리가 다르므로 ball: 2 <br><br>

![image](https://github.com/gkstmdrb/numberbaseballgame/assets/114748816/903c05d4-9708-41b8-bf0c-96948f808d36) <br>
2: 4 5 6을 입력하면 5를 포함하고 자리가 같으므로 strike: 1 <br><br>

![image](https://github.com/gkstmdrb/numberbaseballgame/assets/114748816/ad179da3-2e39-419a-adb9-f88fcf6db65b) <br>
3: 2 3 4를 입력하면 2를 포함하고 자리가 같으므로 strike: 1 <br><br>

![image](https://github.com/gkstmdrb/numberbaseballgame/assets/114748816/afdf623d-f930-42d5-8fbe-147a48be226f) <br>
4: 3 1 6을 입력하면 1을 포함하고 자리가 다르므로 ball: 1 <br><br>

![image](https://github.com/gkstmdrb/numberbaseballgame/assets/114748816/8bba2ae6-8449-481e-9a9b-7d0cf4f101ad) <br>
5: 2 3 5를 입력하면 2는 자리가 같고 5는 자리가 다르므로 strke: 1, ball: 1 <br><br>

![image](https://github.com/gkstmdrb/numberbaseballgame/assets/114748816/3cd22b1c-cac0-4bf6-8fcc-f381f7f8fc0b) <br>
6: 정답인 2 5 1을 입력하였으니 반복문은 종료되고, 시도 횟수가 6회이므로 "보통이네요!"를 출력한다.

<br><br><br>

# 설계
<br>
컴퓨터가 랜덤으로 선택하는 숫자 3개를 넣을 x, y, z를 생성하고, 랜덤값을 넣는다. <br>
이 값을 토대로 사용자가 입력한 숫자와 자리배치를 비교할 com 배열방을 생성한다. <br><br>

``` java
int x, y, z;
Random r = new Random();
x = Math.abs(r.nextInt() % 9) + 1; 
do {
    y = Math.abs(r.nextInt() % 9) + 1;
    } while (y==x); 
do {
    z = Math.abs(r.nextInt() % 9) + 1;
    } while ((z==x)||(z==y));
```
<br><br>


게임 시도 횟수를 세는 count방과 숫자 매칭에 따른 결과를 나타낼 strike, ball 방을 생성한다. <br><br>
------------------------------------------
``` java
int count, strike, ball;
```
<br><br>


사용자가 입력한 값을 저장 할 user 방과 그 입력한 값을 넣을 usr 배열방을 생성한다. <br><br>
------------------------------------------
``` java
int[] usr = new int[3];
int[] com = {x, y, z};
```
<br><br>


사용자가 입력한 3개의 숫자를 usr 배열방에 넣는다. <br><br>
------------------------------------------
``` java
do {
    BufferedReader in = new BufferedReader(new InputStreamReader(System.in));
    String user;
    
    System.out.print("1번째 숫자: ");
    user = in.readLine(); 
    usr[0] = new Integer(user).intValue(); 
    
    System.out.print("2번째 숫자: ");
    user = in.readLine();
    usr[1] = new Integer(user).intValue();
    
    System.out.print("3번째 숫자: ");
    user = in.readLine();
    usr[2] = new Integer(user).intValue();
```
<br><br>

입력한 값이 중복이 되지 않고 1-9까지 범위에서만 입력할 수 있도록 if문을 사용한다. <br>
모든 숫자가 1-9사이, 같은 숫자가 없는 경우에만 반복문을 빠져나온다. <br><br>
------------------------------------------
``` java
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
```
<br><br>

usr, com 두 개의 배열이 각각 완전히 일치할 경우에만 strike 처리를 하고, <br>
usr, com 두 개의 배열의 데이터 위치가 다른 경우에는 ball로 처리를 한다. <br><br>
------------------------------------------
``` java
if (usr[0]==com[0]) strike++;
if (usr[1]==com[1]) strike++;
if (usr[2]==com[2]) strike++; 

if(usr[0]==com[1]) ball++;
if(usr[0]==com[2]) ball++;
if(usr[1]==com[0]) ball++;
if(usr[1]==com[2]) ball++;
if(usr[2]==com[0]) ball++;
if(usr[2]==com[1]) ball++;
```
<br><br>

시도 횟수를 if문으로 판별하여 아래 텍스트를 출력한다.
------------------------------------------
``` java
public static void main(String[] args) throws IOException {
			
		int result; //게임 결과값을 위한 변수 생성
			
		if (args.length==3) { 
			// 게임실행 주어진 3개인 경우, 각각 정수형으로 형변환을 통해 x,y,z 에 저장
			int x = Integer.valueOf(args[0]).intValue();
			int y = Integer.valueOf(args[1]).intValue();
			int z = Integer.valueOf(args[2]).intValue();
			
			result = playGame(x, y, z);
		} else { 				 // 난수발생시키는 경우 즉, playGame()에 해당
			result = playGame(); // return 값 즉, 시도횟수(count)를 결과값으로 반환하여 result에 저장
		}
			
		System.out.println();
		if (result<=2) {
			System.out.println("참 잘했어요!"); //시도횟수가 2번 이하
		} else if (result<=5){
			System.out.println("잘했어요!"); 		 //시도횟수가 3번부터 5번 이하
		} else if (result<=9){
			System.out.println("보통이네요!"); 		 //시도횟수가 6번~9번
		} else {
			System.out.println("분발하세요!");		 //시도횟수가 10번
		}
	}
```
