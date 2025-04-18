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
