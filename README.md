# MemFile2 (MMF) Memory Mapped File 
메모리에 파일을 매핑하여 프로세스간 통신 IPC(InterProcess Communication) 하는 방식이다.  

순서  
1. 파일 매핑 오브젝트를 만든다. (파일 정보를 가짐)  
`<hFMap=CreateFileMapping(hFile, NULL, PAGE_READONLY, 0, 0, NULL);>`  
2. 파일 매핑 오브젝트를 프로세스의 가상 메모리의 주소 공간에 연결한다. (파일뷰)  
`<PtrInFile=(TCHAR *)MapViewOfFile(hFMap, FILE_MAP_READ,0,0,0)>`  
TCHAR 말고 BYTE로 형변환해서 사용도 가능(아래링크 참고)  
(참고) TCHAR 란 wide char 를 의미한다.(안시코드,유니코드 다 포괄)  
https://github.com/ohjiwoo123/AsynciO/blob/master/AsynciO/AsynciODlg.cpp  
3. 파일을 메모리처럼 사용한다.
`<strcpy(PtrInFile, “hello”, 5);>`  
4. 파일뷰를 닫는다.  
`<UnmapViewOfFile(PtrInFile);>`
