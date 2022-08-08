- 👋 Hi, I’m @tarungk
- 👀 I’m interested in ...
- 🌱 I’m currently learning ...
- 💞️ I’m looking to collaborate on ...
- 📫 How to reach me ...

<!---
tarungk/tarungk is a ✨ special ✨ repository because its `README.md` (this file) appears on your GitHub profile.
You can click the Preview link to take a look at your changes.
--->

                                 VIRTUAL PIANO 
  
   Our project "Virtual Piano" is a simple graphical user interface application using C++  language. 
   It is pretty much an electronic piano which maps the piano sounds with the keys on the keyboard. 
   The purpose of this virtual  piano is to provide a playable piano allowing any user to play the piano without advanced knowledge of C++ language. 
   The design of the virtual piano action is composed of a virtual keyboard with 7 frequencies and having audio capabilities. 
   The best part of this application is ,  a person can play it anywhere as he/she will just need a desktop/ laptop and Turbo C installed in their system. 
   At last , this is absolutely free of cost and portable. 
  
 */ 
  
 /* Header Files */ 
  
 #include<iostream.h> 
 #include<dos.h> 
 #include<conio.h> 
 #include<stdlib.h> 
 #define SHOW 1 
 #define HIDE 2 
 union REGS input,output; 
  
 class piano 
 { 
  public:int BIGKEY,MIDKEY,back,border; 
         piano()  /* Constructor initialization */ 
         { 
                 BIGKEY=15; 
                 MIDKEY=1; 
                 back=7; 
                 border=15; 
         } 
 }color; 
  
 void drawpiano(int x,int y); 
 int check_xy(int x,int y); 
 void BOX(int c,int r,int c1,int r1,int col); 
 int initmouse(); 
 void setupscreen(); 
 void pointer(int on); 
 void restrictmouse(int x1,int y1,int x2,int y2); 
 void check_keys(int x,int y); 
 void getmouse(int *button,int *x,int *y); 
 float freq[7] = {130.81, 146.83, 164.81, 174.61,196, 220, 246.94 } ; 
 int n=0,a=4,backcolor=2,exitcode=1; 
 void showbar(int t) 
 { 
  if(t>65) t=65; 
  if(t<1) t=1; 
  textcolor(15); 
  for(int q=0;q<=t;t++) 
  { 
         gotoxy(3+q,4); 
         cprintf("Û"); 
  } 
 } 
  
  
 int main() 
 { 
  int b,x,y,key; 
  char ch; 
  if(initmouse()==-1) /* Terminates the program if mouse not connected */ 
  { 
         clrscr(); 
         cout<<"\n\nNO MOUSE !\n\n"; 
         exit(1); 
  } 
  pointer(SHOW); 
  setupscreen(); 
  exitcode=1; 
  while(exitcode) 
  { 
         if(kbhit()) 
         { 
            ch=getch(); 
            if(ch==27) break; 
            if(ch==75) a--; 
            if(ch==77) a++; 
            check_keys(x,y); 
            switch(ch) 
            { 
                 case 'a':case'A':key=0;break; 
                 case 's':case'S':key=1;break; 
                 case 'd':case'D':key=2;break; 
                 case 'f':case'F':key=3;break; 
                 case 'j':case'J':key=4;break; 
                 case 'k':case'K':key=5;break; 
                 case 'l':case'L':key=6;break; 
            } 
            sound(freq[key]*a); 
            delay(80); 
            nosound(); 
         } 
         getmouse(&b,&x,&y); 
         if(b==1) 
         { 
                 while(b==1) 
                 { 
                         getmouse(&b,&x,&y); 
                         key=check_xy(x,y); 
                         if(key!=-1 && key<7) 
                         { 
                                 sound(freq[key]*a); 
                         } 
                         else if(key>6) 
                              { 
                                  sound(freq[12-key]*(a/2)); 
                              } 
                 } 
                 nosound(); 
                 check_keys(x,y); 
         } 
  } 
  textbackground(0); 
  clrscr(); 
  _setcursortype(_NORMALCURSOR); 
 return 0; 
 } 
  
 /* End of Main Function */ 
  
 void setupscreen() /* Display screen settings */ 
 { 
  _setcursortype(_NOCURSOR); 
  textbackground(backcolor); 
  clrscr(); 
  drawpiano(9,17); 
  BOX(4,5,8,5,0); 
  BOX(5,5,7,5,1); 
  textcolor(15); 
  gotoxy(70,5); 
  cprintf(">Quit<"); 
  gotoxy(4,4); 
  cprintf("Range"); 
  textbackground(0); 
  gotoxy(8,5); 
  cprintf(""); 
  gotoxy(4,5); 
  cprintf(""); 
  gotoxy(6,5); 
  cprintf("%d",a); 
  textcolor(14); 
  textbackground(backcolor+7); 
  gotoxy(30,4); 
  cprintf(" VIRTUAL PIANO "); 
  
 } 
  
 void pianokey(int x,int y) /* Piano key display settings */ 
 { 
  textbackground(color.MIDKEY); 
  textcolor(color.BIGKEY); 
  gotoxy(x,y); 
  cprintf("ÛÛÛ  ÛÛÛ"); 
  gotoxy(x,y+1); 
  cprintf("ÛÛÛ  ÛÛÛ"); 
  gotoxy(x,y+2); 
  cprintf("ÛÛÛ  ÛÛÛ"); 
  gotoxy(x,y+3); 
  cprintf("ÛÛÛÛÞÛÛÛ"); 
  gotoxy(x,y+4); 
  cprintf("ÛÛÛÛÞÛÛÛ"); 
  gotoxy(x,y+5); 
  cprintf("ÛÛÛÛÞÛÛÛ"); 
  gotoxy(x,y+6); 
  cprintf("ÛÛÛÛÞÛÛÛ"); 
  gotoxy(x,y); 
 } 
  
 void drawpiano(int x,int y) /* Drawing of piano */ 
 { 
  int t=9; 
  BOX(x-5,y-3,75,y+8,color.border); /*invoking function box */ 
  BOX(x-4,y-2,74,y+7,color.back); 
  pianokey(x,y); 
  pianokey(x+t,y); 
  pianokey(x+t*2,y); 
  pianokey(x+t*3,y); 
  pianokey(x+t*4,y); 
  pianokey(x+t*5,y); 
  pianokey(x+t*6,y); 
 } 
  
 void BOX(int c,int r,int c1,int r1,int col) 
 { 
  int i,j; 
  textcolor(col); 
  for(i=r;i<=r1;i++) 
  { 
         for(j=c;j<=c1;j++) 
         { 
                 gotoxy(j,i); 
                 cprintf("Û"); 
         } 
  } 
 } 
 int initmouse() 
 { 
  input.x.ax=0; 
  int86(0x33,&input,&output); 
  return(output.x.ax==0 ? -1 : 0); 
 } 
 void pointer(int on) 
 { 
    input.x.ax=on; 
    int86(0x33,&input,&output); 
 } 
 void restrictmouse(int x1,int y1,int x2,int y2) 
 { 
    input.x.ax=7; 
    input.x.cx=x1/8; 
    input.x.dx=x2/8; 
    int86(0x33,&input,&output); 
    input.x.ax=8; 
    input.x.cx=y1/8; 
    input.x.dx=y2/8; 
    int86(0x33,&input,&output); 
 } 
 void getmouse(int *button,int *x,int *y) 
 { 
   input.x.ax=3; 
   int86(0x33,&input,&output); 
   *button=output.x.bx; 
   *x=output.x.cx/8; 
   *y=output.x.dx/8; 
 } 
 int check_xy(int x,int y) 
 { 
   /* Mid keys */ 
   if(x>=11 && y>=16 && x<=12 && y<=18) 
   return 7; 
   if(x>=20 && y>=16 && x<=21 && y<=18) 
   return 8; 
   if(x>=29 && y>=16 && x<=30 && y<=18) 
   return 9; 
   if(x>=38 && y>=16 && x<=39 && y<=18) 
   return 10; 
   if(x>=47 && y>=16 && x<=48 && y<=18) 
   return 11; 
   if(x>=56 && y>=16 && x<=57 && y<=18) 
   return 0; 
   if(x>=65 && y>=16 && x<=66 && y<=18) 
   return 12; 
  
   /* Big keys */ 
   if(x>=8 && y>=16 && x<=15 && y<=22) 
   return 0; 
   if(x>=17 && y>=16 && x<=24 && y<=22) 
   return 1; 
   if(x>=26 && y>=16 && x<=33 && y<=22) 
   return 2; 
   if(x>=35 && y>=16 && x<=42 && y<=22) 
   return 3; 
   if(x>=44 && y>=16 && x<=51 && y<=22) 
   return 4; 
   if(x>=53 && y>=16 && x<=60 && y<=22) 
   return 5; 
   if(x>=62 && y>=16 && x<=69 && y<=22) 
   return 6; 
   return (-1);  /*no key pressed */ 
 } 
 void check_keys(int x,int y) 
 { 
   if(x==7 && y==4)  a++; 
   if(x==3 && y==4)  a--; 
   if(a<1) a=1;else if(a>30) a=30; 
   textcolor(15);textbackground(1); 
   gotoxy(5,5);cprintf("   "); 
   if(a<10) gotoxy(6,5); 
   else gotoxy(5,5); 
   cprintf("%d",a); 
   if(x>=69 && y>=4 && x<=74 && y<=4) exitcode=0; 
 } 
 //****************************END OF PIANO***********************************************// 
 
