
다음과 같이 해보세요
1. 폴더를 생성함 (이왕이면 아주 간단한 이름)
2. 폴더에 해당 zip 파일을 압축해제함
3. cmd] go build [enter] 를 수행함
4. 폴더명.exe 파일이 생성됨을 확인함
5. 폴더 밑에 test 폴더를 생성하고, test폴더 밑에 4개의 폴더를 신규로 생성함
   폴더명은 node의 포트번호로 설정함
   예) node IP = 127.0.0.1:5000 일 경우, 폴더명 = '5000'
6. 이제 폴더명.exe 파일을 test / 5000, 4000, 5001, 4001 등 폴더에 복사함
7. 4개의 폴더, 4개의 포트번호 중 하나를 <리더노드>로 선택함
   ==> 이 <리더노드>의 주소와 <그 외 노드들>의 주소값을 기입해놓음
8. 소스 network/node.go 파일을 열어서 
-----------------------------------------------------------
func NewNode(nodeID string) *Node {
	const viewID = 10000000000 // temporary.

	node := &Node{
		// Hard-coded for test.
		NodeID: nodeID,
		NodeTable: map[string]string{
			"Apple": "localhost:1111",   <------노드 주소값을 변경해줌
			"MS": "localhost:1112", <------노드 주소값을 변경해줌
			"Google": "localhost:1113", <------노드 주소값을 변경해줌
			"IBM": "localhost:1114", <------노드 주소값을 변경해줌
		},
		View: &View{
			ID: viewID,
			Primary: "Apple", <------리더노드 주소명을 써 줌
		},
-----------------------------------------------------------------------
위와 같이 코드 수정 후 저장
9. 위의 3, 4번을 수행함
10. 위의 6번을 수행함
11. 각 하위 폴더에서 cmd 창에서 다음과 같이 동작시킴
      cmd > 폴더명.exe 5000  [enter]   <---- 포트번호
     이렇게 4개의 서버를 동작 시킴
    ===> 4개의 서버(노드)가 스탠바이 상태가 됨

---------------------------------------------------------------------------------
12. <리더노드>에게 명령(tx)을 전송할 차례입니다
     curl을 설치하세요
13. curl을 이용하여 그림파일 working-screenshot.png 의 왼쪽 상단에 나온 curl 명령문을
     그대로 복사해서 전송함
---------------------------------------------------------------------------------

14. log 문을 화면에 출력하면서 동작을 확인함

---------------------------------------------------------------------------------     










