# 4주차 - 자료구조와 알고리즘
•순차자료구조: 같은 자료구조에 속한 원소들을 일렬로 연속해서 저장함

-장점: 특정 원소 탐색이 빠르다

-단점: 메모리 낭비가 발생할 수 있다. /
         중간에 있는 원소 삽입, 삭제가 어렵다
```
ex) 
int a[3,4,5]
  
a[2] = 10   --> 3번쩨 원소를 10으로 바꿈

int = 4바이트

a가 100번지에 위치

= 100 + 4 *2 => 108번지 
```

# 연결리스트 주석달기
``` python
''' 단순연결리스트를 이용한 객체지향 전화번호부 자료관리.
- 단순연결리스트 클래스에 노드 클래스를 삽입
- 이름 중복 체크
- 이름순으로 연결리스트에 저장
- 24.04.15
'''

class PhoneBook:
        class Node:
                def __init__(self, data):
                        self.data = data 
                        self.next = None
		
        def __init__(self):
                self.head = None #연결리스트 초기화


        def insertNode(self, add_data):                    
                if self.head == None:  # 연결리스트가 비어있으면
                        self.head= self.Node(add_data) # 입력받은 주소값을 헤드가 가르킴
                        print("신규입력 완료\n")
                        return
    
                current = self.head #현재 노드를 헤드로
                prev= None # 이전노드 초기화
                while current :    #노드가 있을때까지
                        if current.data[0] == add_data[0]: # 이미 있는 이름이라면
                                print("이미 있는 이름입니다\n")
                                return
                        elif current.data[0] > add_data[0] : #새로 넣을 이름 값이 더 작으면
                                break
                        prev = current #이전 값을 현재 값으로
                        current = current.next # 현재 값은 다음 노드를 가르킴
                        
                new_node = self.Node(add_data) # 새노드 생성
                
                if not prev : # 가장 작은 이름임 ( 맨 앞에 들어가야할 때)
                        new_node.next = self.head # 새로 추가된 노드는 원래 리스트의 첫번째 값 주소를 가짐
                        self.head = new_node # 헤드가 새로 추가된 노드의 주소값을 가르킴

                else : #중간에 삽입되어야 할 때
                        prev.next = new_node # 앞에 위치할 노드는 삽입할 노드의 주소를 가르킴
                        new_node.next = current #삽입할 노드가 다음(이름 값이 더 큰) 노드의 주소를 가르킴
                print("신규입력 완료\n")
                
        def changeNode(self, change_name):
                current = self.head #첫번째 노드를 current
                while current : # 입력한 이름을 찾을 때까지
                        if current.data[0] == change_name: # 이름이 같으면
                                print("\n{}전화번호는 {}입니다.".format(current.data[0], current.data[1])) # 이름, 전화번호
                                current.data[1] = input("변경할 전화번호:") # 전화번호 변경
                                print("\n{}의 전화번호가 {}으로 수정되었습니다.".format(current.data[0], current.data[1]))
                                return
                        current=current.next # 현재값은 다음 노드를 가르킴
                print("없는 이름입니다\n")
                
                      
    
        def printNodes(self): # 전체 출력
                current = self.head #current= 첫번째 노드
                if current == None:  # 빈 리스트이면
                        return 
                while current != None: # 빈 리스트가 아니면
                        print(current.data, end = ' ') 
                        current = current.next # 순차적으로 출력
               
                return
                

         
        def deleteNode(self, delete_name): # 노드 삭제
                if self.head == None: # 빈 연결리스트
                        print("연결리스트가 비어 있습니다\n")
                        return
                current = self.head #current는 첫번째 노드
                prev = None # 초기화
  	  
                while current : # 같은 이름 찾기
                        if current.data[0] == delete_name :  # 이름이 같으면
                                if not prev:  # 첫번째 자료임
                                        self.head = current.next # 첫번째 노드가 원래 첫번째 노드의 다음 노드로 바뀜
                                else :
                                        prev.next = current.next # 삭제할 노드의 앞 노드가 삭제할 노드의 뒷 노드의 주소를 가르킴
                                del current  # 해당 노드를 메모리에서 free시킴
                                print("연락처가 삭제되었습니다\n")
                                return
                        prev = current  # 다음 노드로 이동
                        current = current.next # 다음 노드 주소를 current에
                
                print("없는 이름 입니다\n")


                

        def findNode(self,find_name): # 이름 찾기
                if self.head == None: # 빈 리스트
                        print("빈 리스트입니다")
                        return None
                current = self.head # 첫번째 노드

                while current :
                        if current.data[0] > find_name: # 찾으려는 이름이 첫번째 노드보다 작으면
                                
                                break; # 없는 이름
                        
                        if current.data[0] == find_name: #찾는 이름을 current가 가지고 있다면
                                print('\n{}님의 전화번호는 {} 입니다.' .format(current.data[0], current.data[1]))
                                return current
                        current = current.next # current가 다음 노드의 주소를 가짐.
                print("없는 이름입니다\n")
                return None

	    
if __name__=="__main__":

    print('단순연결리스트를 이용한 전화번호부 관리 프로그램입니다.\n')
    
    P = PhoneBook()  # 단순연결리스트 생성

    while True:
        print('\n1: 입력\t 2:수정\t 3:삭제\t 4:탐색\t 0:종료\n')
        
        ch = input("기능 선택--> ")
            
        if ch == '0':
            P.printNodes()
            print('종료합니다\n')
            break

        elif ch == '1':
            add_data =[]
            add_data.append(input('입력할 이름: '))         
            add_data.append(input('입력할 전화번호: '))
            P.insertNode(add_data) 
            P.printNodes()
            
        elif ch == '2':
            change_name = (input('전화번호를 수정할 이름:'))
            P.changeNode(change_name)  
            P.printNodes()

        elif ch == '3':
            delete_name = input('삭제할 이름: ')
            P.deleteNode(delete_name)                            
            P.printNodes()
            
        elif ch == '4':
            search_name = input('탐색할 이름 : ')
            P.findNode(search_name)
        else:       
            print('\n잘못된 입력입니다.\n')

    

```

# 5주차 - 스텍
```
스택
= 선형 자료구조 (1:1)
= 자료간의 관계가 1:1 인 선형구조 중 하나로 자료의 입출력이 한쪽 끝에서만 발생하도록 제한한 구조
- LIFO
push() -> 삽입(함수)
pop() -> 아웃(함수)
top -> 가장 위의 원소
```
# 6주차 - 스텍
u배열의 장단점
- 장점
1. 시작위치, 크기, 인덱스를 알기 때문에 특정 원소의 검색이 빠름
2. 리스트 크기의 변경이 없을 때, 중간 원소 삽입/삭제가 없을 때 사용하면 좋음
- 단점
1. 중간 원소를 삽입하거나 삭제할 때 불필요한 오버헤드가 발생
2. 리스트 :0~n, 인덱스 :k인 경우
3. 삽입: 새 원소를 위해 n-k+1개 원소가 뒤로 이동하는 오버헤드
4. 삭제 : n-k개 원소가 삭제된 원소 자리를 채우기 위해 앞으로 이동하는 오버헤드 발생
u연결리스트(linked list)의 장단점
- 장점
1. 메모리활용 효율적
- 단점
1. 특정원소를 찾기가 어려움
2. 각각의 원소들이 자기 다음 원소의 위치를 알고 있어야 함
✅ 연결리스트 전화번호부 프로그램
1. 클래스 초기화 (__init__)
- PhoneBook클래스는 연결리스트를 이용한 전화번호부를 관리
- Node클래스는 연결리스트의 각 노드를 나타내며, 각 노드는 data(이름, 전화번호)를 저장하고
next로 다음 노드를 가리킴
2. 전화번호부에 데이터 삽입 (insertNode)
- insertNode메소드는 새로운 연락처를 전화번호부에 삽입
- 이름 순으로 정렬하여 삽입하며, 이미 존재하는 이름이 입력되면 삽입을 거부하고 메시지를 출력
- 만약 삽입할 이름이 리스트의 첫 번째 이름보다 작으면 head에 새로운 노드를 삽입하고,
중간에 삽입할 경우 기존 노드 사이에 새로운 노드를 추가
3. 전화번호 수정 (changeNode)
- changeNode메소드는 사용자가 지정한 이름에 해당하는 전화번호를 수정
- 이름을 찾으면 기존의 전화번호를 출력하고, 새 전화번호를 입력받아 수정
4. 전화번호 출력 (printNodes)
- printNodes메소드는 전화번호부에 저장된 모든 노드를 출력
- 연결리스트를 순차적으로 탐색하며 각 노드의 데이터를 출력
5. 전화번호 삭제 (deleteNode)
- deleteNode메소드는 사용자가 지정한 이름을 가진 노드를 삭제.
- 삭제할 노드가 첫 번째 노드인 경우 head를 갱신하고, 중간 노드인 경우 이전 노드의 next를 수정
6. 전화번호 탐색 (findNode)
- findNode메소드는 사용자가 지정한 이름을 가진 노드를 찾아 전화번호를 출력
- 이름이 알파벳 순으로 정렬되어 있기 때문에, 만약 찾고자 하는 이름이 현재 노드보다 작으면
탐색을 중단
u실행 흐름
- 프로그램은 무한 루프 안에서 사용자의 입력을 기다리며, 입력된 기능에 따라 연락처를 추가, 수정,

스택
= 선형 자료구조 (1:1)
= 자료간의 관계가 1:1 인 선형구조 중 하나로 자료의 입출력이 한쪽 끝에서만 발생하도록 제한한 구조
- LIFO
push() -> 삽입(함수)
pop() -> 아웃(함수)
top -> 가장 위의 원소 

-------> 배열로 처리함 (이유: 위 아래로만 꺼내기 때문에?)
 후위 수식 
= 43* 72/ - (-> 4와 3을 곱하고 7과 2를 나누고  그 두개를 뺀다)
전위수식

A*B/C + D*E -F
-> AB*C/ DE*  +  F- =후위 수식
-+/*ABC *DEF = 전위수식

계산기 프로그램: 중위수식 -> 후위수식 -> 후위수식 계산 : 화살표 두번 스택을 사용

---

# 시험 문제 풀이
1번
배열
- 장점: 구현이 용이하고 특정원소 탐색이 쉬움
-단점: 중간에 원소 삽입, 삭제가 어려움, 메모리 사용 비효율적

연결리스트
-장점: 중간에 원소 삽입 삭제가 편리함, 메모리 사용 효율적
- 단점: 구현이 어려움, 특정 원소의 탐색이 어려움


스택: LIFO 역순 문자열, 후위 수식 계산
큐: FIFO 프린터큐, 들어온 순서대로 처리해야하는 데이터 저장



2번
배열: 인덱스를 이용( 인덱스에 위치 더하기) , 특정 원소 바로 검색
연결자료구조: head가 가르키는 첫번째 노드부터 순차 검색
head 부터 시작해서 차례대로 하나씩 읽는 방법 밖에 없음
-> 그림은 3장 참고

3번
빅오-시간복잡도

4번 전위/후위
A - B * C / E + F/G - H
전위:+-A/*BCE/FGH
후위: ABC*E/- FG/+ H -

5번
큐를 1차원배열(순차리스트)

초기화 = -1
front= rear -> 비어있다
rear= n-1 -> 배열이 꽉 찼다

자리가 비어있음에도 rear= n-1이 되면 포화 상태로 인식
-> 빈 공간을 활용하기 위해 원형큐 생성



self.PhoneBook([name, phone])

for i in self.PhoneBook :
		if(i[0] == name):
			position= count
			break
		else: 
			count= count +1


del(self.PhoneBook[position])


if self.head ==None:
	self.head ==self.Node(add_data)





if not prev:
	 new_node.next= self.head
	 self.head= new_node

else: 
	prev.next= new_node
	new_node.next=current

 # 8주차- 트리
 BST,heap


BST
 완전 이중구조
 : 왼쪽부터 차례로 채우기

 heap
 : 루트를 지워가면서 비교 후 출력
 - 사람이 하명 오래걸리지망 컴토는 빠름
 - 

 연습문제 풀어보기
 # 그래프
 
