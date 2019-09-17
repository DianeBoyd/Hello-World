S T="0008,0020",I=0 ; R  Study Date
 S P="" F  S P=$O(REQ(T,P))   Q:P=""  D:REQ(T,P)'=""
 . N FR,UT
 . S I=I+1 I I>1 D ERR^MAGDQRUE("More than one study date specified.") Q
 . S (X,FR,UT)=REQ(T,P) S:X["-" FR=$P(X,"-",1),UT=$P(X,"-",2)
 . I FR'="",FR'?8N D ERR^MAGDQRUE("Invalid 'from' date: """_FR_""".")
 . I UT'="",UT'?8N D ERR^MAGDQRUE("Invalid 'until' date: """_UT_""".")
 . S FD=+FR S:FD FD=FD-17000000
 . I UT'="" S LD=+UT S:LD LD=LD-17000000  ;P239;DSB-Fix last date when null
 . I UT="" S LD=$$HTFM^XLFDT($H,1)
 . S TIM=1
 . Q
 ;
