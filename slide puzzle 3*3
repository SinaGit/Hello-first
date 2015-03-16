#include <stdio.h>
#include <conio.h>
#include <stdlib.h>
#include <windows.h>

#define UP                  0
#define DOWN                1
#define LEFT                2
#define RIGHT               3

void update_screen(void);
void swap_num(int * a1,int * a2);
void swap_handle(int add1,int add2);
void initiate_with_standard(void);
void get_table(void);
void delay(void);
void find_xy(int number,int *px,int *py);
void move_zero(int px,int py,int no_touch_x,int no_touch_y);
void move_tile(int p1x,int p1y,int p2x,int p2y);
void solve(void);

int x[3][3];
char ff=0;

int main(int argc, char *argv[])
{
    /*unsigned char t;
    do
    {
    t=getch();
    printf("%d\n",t);
    } while (1) ;*/
    initiate_with_standard();
    update_screen();
    
    update_screen();
    
    get_table();
    
    delay();
    update_screen();
    
    delay();
    //move_zero(1,1,0,1);
    //move_tile(2,1,0,0);
    //move_zero(0,1,0,0);
    solve();
    
    printf("\n");
    system("PAUSE");	
    return 0;
}

// ---------------------------------------------------------------- //

void swap_num(int *a1, int *a2)
{
     int x=*a1;
     *a1=*a2;
     *a2=x;
}

// ---------------------------------------------------------------- //

void update_screen(void)
{
     int i,j;
     system("cls");
     
     for (i=0;i<3;i++)
     {
         for (j=0;j<3;j++)
         {
             if (x[i][j] != 0)
                printf("%2d ",x[i][j]);
             else
                printf("   ");
             if (j < 2) printf("|");
         }
         if (i<2) printf("\n--- --- ---\n");
     }
}

// ---------------------------------------------------------------- //

void initiate_with_standard(void)
{
     int i,j;
     for (i=0;i<3;i++)
         for (j=0;j<3;j++)
             x[i][j] = (i*3) + (j) + 1;
     x[2][2]=0;
}

// --------------------------------------------------------------- //

void get_table(void)
{
     int i,j,k,f=0,rc_cnt=0;
     int tmp_i,tmp_j;
     unsigned char c=' ';
     system("cls");
     
     for (i=0;i<3;i++)
         for (j=0;j<3;j++)
         x[i][j]=0;
         
     i=j=0;
     k=1;
     do
     {
         x[i][j]=k;
         update_screen();
         c=getch();
         if (c!=13) c=getch();
         switch (c)
         {
                case 13:  
                          // Enter
                          f=3;
                          for (i=0;i<3;i++)
                              for (j=0;j<3;j++)
                                  if (x[i][j]==0)
                                  {
                                      f=i;
                                      i=4;
                                      break;
                                  }
                          i=f;
                          k++;
                          break;
                case 72:  // up
                          /*if (i>0 && x[i-1][j]==0)
                          {
                              x[i-1][j]=k;
                              x[i][j]=0;
                              i--;
                          }*/
                          /*for (rc_cnt=i-1;rc_cnt>=0;rc_cnt--)
                          {
                              if (x[rc_cnt][j]==0)
                              {
                                  x[rc_cnt][j]=k;
                                  x[i][j]=0;
                                  i=rc_cnt;;
                                  break;
                              }
                          }*/
                          break;
                case 80: 
                          // down
                          /*if (i<3 && x[i+1][j]==0)
                          {
                             x[i+1][j]=k;
                             x[i][j]=0;
                             i++;
                          }*/
                          break;
                case 77: 
                          // right
                          tmp_i=i;
                          tmp_j=j;
                          for (i=i;i<3;i++,j=0)
                          {
                              for (j=j;j<3;j++)
                              {
                                  if (x[i][j] == 0)
                                  {
                                     x[i][j] = x[tmp_i][tmp_j];
                                     x[tmp_i][tmp_j]=0;
                                     tmp_i=i;
                                     tmp_j=j;
                                     i=j=4;
                                  }
                              }
                          }
                          i=tmp_i;
                          j=tmp_j;
                          break;
                case 75: 
                          // left
                          tmp_i=i;
                          tmp_j=j;
                          for (;i>=0;i--,j=2)
                          {
                              for (;j>=0;j--)
                              {
                                  if (x[i][j]==0)
                                  {
                                       x[i][j]=x[tmp_i][tmp_j];
                                       x[tmp_i][tmp_j]=0;
                                       tmp_i=i;
                                       tmp_j=j;
                                       i=-1;
                                       j=-1;
                                  }
                              }
                          }
                          i=tmp_i;
                          j=tmp_j;
                          break;
         }
     }
     while (k < 9) ;
}

// -------------------------------------------------------------- //

void swap_handle(int add1,int add2)
{
     swap_num(&x[add1/3][add1%3] , &x[add2/3][add2%3]);
}

// -------------------------------------------------------------- //

void find_xy(int number,int *px,int *py)
{
     int i,j;
     
     for (i=0;i<3;i++)
     {
         for (j=0;j<3;j++)
         {
             if (x[i][j]==number)
             {
                 *px=i;
                 *py=j;
                 break;
             }
         }
     }
}

// ----------------------------------------------------------------- //
void move_zero(int px,int py,int no_touch_x,int no_touch_y)
{
     int db_x,db_y,i,j,k,pcnt=0,path[20];
     int dx,dy,fx,fy,zx,zy,tzx,tzy;
     
     find_xy(0,&zx,&zy);
     db_x=tzx = zx;
     db_y=tzy = zy;
     dx = px - zx;
     dy = py - zy;
     fx = (dx > 0) ? 1:-1 ;
     fy = (dy > 0) ? 1:-1 ;
     if (dx==0) fx=0;
     if (dy==0) fy=0;
     //printf("\n\n\n\nfx=%d , tzx=%d , px=%d\n",fx,tzx,px);
     //printf("\ndx=%d,dy=%d",dx,dy);
     //delay();//delay();delay();
     while ( ((tzx!=px) || (tzy!=py) ) && (pcnt<20) )
     {
           //printf("fx=%d,fy=%d",fx,fy);
           //delay();
           if ( (fx>0) && (no_touch_x == tzx+1) && (tzy==no_touch_y) )
           {
                /*  D
                    X
                */
                //path[pcnt++] = (tzy==0) ?  RIGHT : LEFT  ;
                if (tzy==0)
                {
                   path[pcnt++] = RIGHT;
                   tzy++;
                }
                else
                {
                    path[pcnt++] = (fy > 0) ? RIGHT : LEFT ;
                    tzy          = (fy > 0) ? tzy+1 : tzy-1 ;
                }
                //tzy          = (tzy==0) ?  tzy+1 : tzy-1 ;
                path[pcnt++] = DOWN;
                tzx++;
                //printf("\npcnt=%d => 1",pcnt);
                //delay();delay();
           }
           else if ( (fx>0) )//&& (no_touch_x != tzx+1) )
           {
                /*   D
                     
                */
                path[pcnt++]=DOWN;
                tzx++;
                //printf("\npcnt=%d => 2",pcnt);
                //delay();delay();
           }
           else if ( (fx<0) && (no_touch_x == tzx-1) && (tzy==no_touch_y) )
           {
                /*   X
                     U
                */
                //path[pcnt++] = (tzy==0) ?  RIGHT : LEFT  ;
                if (tzy==0)
                {
                   path[pcnt++] = RIGHT;
                   tzy++;
                }
                else
                {
                    path[pcnt++] = (fy > 0) ? RIGHT : LEFT ;
                    tzy          = (fy > 0) ? tzy+1 : tzy-1 ;
                }
                //tzy          = (tzy==0) ?  tzy+1 : tzy-1 ;
                path[pcnt++] = UP;
                tzx--;
                //printf("tzy=%d,py=%d",tzy,py);
                //printf("\npcnt=%d => 3",pcnt);
                //delay();delay();
           }
           else if ( (fx<0))// && (no_touch_x != tzx-1) )
           {
                /*   
                     U
                */
                path[pcnt++] = UP;
                tzx--;
                //printf("\npcnt=%d => 4",pcnt);
                //delay();delay();
           }
           else if ( (fy>0) && (no_touch_y == tzy+1) && (tzx==no_touch_x) )
           {
                /*   
                     R  X
                     
                */
                //path[pcnt++] = (tzx==0) ? DOWN  : UP ;
                //tzx          = (tzx==0) ? tzx+1 : tzx-1 ;
                if (tzx==0)
                {
                   path[pcnt++] = DOWN;
                   tzx++;
                }
                else
                {
                    path[pcnt++] = (fx > 0) ? DOWN  : UP    ;
                    tzx          = (fx > 0) ? tzx+1 : tzx-1 ;
                }
                path[pcnt++] = RIGHT;
                tzy++;
                //printf("\npcnt=%d => 5",pcnt);
                //delay();delay();
           }
           else if ( (fy>0))// && (no_touch_y != tzy+1) )
           {
                /*   
                     R
                     
                */
                path[pcnt++] = RIGHT;
                tzy++;
                printf("\npcnt=%d => 6",pcnt);
                delay();delay();
           }
           else if ( (fy<0) && (no_touch_y == tzy-1) && (tzx==no_touch_x) )
           {
                /*   
                     X   L
                     
                */
                //path[pcnt++] = (tzx==0) ? DOWN  : UP ;
                //tzx          = (tzx==0) ? tzx+1 : tzx-1 ;
                if (tzx==0)
                {
                   path[pcnt++] = DOWN;
                   tzx++;
                }
                else
                {
                    path[pcnt++] = (fx > 0) ? DOWN  : UP    ;
                    tzx          = (fx > 0) ? tzx+1 : tzx-1 ;
                }
                path[pcnt++] = LEFT;
                tzy--;
                //printf("\npcnt=%d => 7",pcnt);
                //delay();delay();
           }
           else if ( (fy<0))// && (no_touch_y != tzy-1) )
           {
                /*   
                         L
                     
                */
                path[pcnt++] = LEFT;
                tzy--;
                //printf("tzy=%d,py=%d",tzy,py);
                //delay();delay();
                //printf("\npcnt=%d => 8",pcnt);
                //delay();delay();
           }
           
           
           dx = px - tzx;
           dy = py - tzy;
           fx = (dx > 0) ? 1:-1 ;
           fy = (dy > 0) ? 1:-1 ;
           if (dx==0) fx=0;
           if (dy==0) fy=0;
           if (tzx==px) fx=0;
           if (tzy==py) fy=0;
     }
     if (pcnt==20)
     {
        printf("\n\npcnt=20 \nmoving zero to desired destinition ERROR!");
        printf("\nzero from pos[%d][%d] to pos[%d][%d]",db_x,db_y,px,py);
        printf("\ndont touch = pos[%d][%d]",no_touch_x,no_touch_y);
        for (i=0;i<10;i++)
        {
            switch (path[i])
            {
                   case UP:    printf("\nUP");    break;
                   case DOWN:  printf("\nDOWN");  break;
                   case LEFT:  printf("\nLEFT");  break;
                   case RIGHT: printf("\nRIGHT"); break;
            }
        }
        while (1);
     }
     else
     {
        for (i=0;i<pcnt;i++)
        {
            switch (path[i])
            {
                   case UP:    
                               swap_handle(zx*3+zy , zx*3+zy-3);
                               zx--;
                               break;
                   case DOWN:  
                               swap_handle(zx*3+zy , zx*3+zy+3);
                               zx++;
                               break;
                   case LEFT:  
                               swap_handle(zx*3+zy , zx*3+zy-1);
                               zy--;
                               break;
                   case RIGHT: 
                               swap_handle(zx*3+zy , zx*3+zy+1);
                               zy++;
                               break;
            }
            update_screen();
            delay();
        }
     }
}
// ----------------------------------------------------------------- //

void move_tile(int p1x,int p1y,int p2x,int p2y)
{
     int dx=0,dy=0,zero_x,zero_y,fx,fy;

     
     dx = p2x-p1x ;
     fx = (dx > 0) ? 1 : -1;
     dy = p2y-p1y ;
     fy = (dy > 0) ? 1 : -1 ;
     
     //printf("\nmove tile,dx=%d,dy=%d",dx,dy);
     //delay();
     if (ff==0)
     {
     while (p1x!=p2x)
     {
           
           //printf("x cor");
           //delay();
           //printf("moving zero to pos[%d][%d] (fx=%d)",p1x+fx,p1y,fx);
           //delay();delay();delay();
           move_zero(p1x+fx,p1y,p1x,p1y);
           //printf("zero moved");
           //delay();delay();delay();delay();
           swap_handle(p1x*3+p1y , p1x*3+p1y+fx*3);
           p1x+=fx;
           update_screen();
           //printf("swaped");
           delay();
     }
     
     while (p1y != p2y)
     {
           //printf("y cor");
           //delay();
           move_zero(p1x,p1y+fy,p1x,p1y);
           swap_handle(p1x*3+p1y , p1x*3+p1y+fy);
           update_screen();
           delay();
           p1y+=fy;
     }
     ff=1;
     }
     else
     {
     while (p1y != p2y)
     {
           //printf("y cor");
           //delay();
           move_zero(p1x,p1y+fy,p1x,p1y);
           swap_handle(p1x*3+p1y , p1x*3+p1y+fy);
           update_screen();
           delay();
           p1y+=fy;
     }
     while (p1x!=p2x)
     {
           
           //printf("x cor");
           //delay();
           //printf("moving zero to pos[%d][%d] (fx=%d)",p1x+fx,p1y,fx);
           //delay();delay();delay();
           move_zero(p1x+fx,p1y,p1x,p1y);
           //printf("zero moved");
           //delay();delay();delay();delay();
           swap_handle(p1x*3+p1y , p1x*3+p1y+fx*3);
           p1x+=fx;
           update_screen();
           //printf("swaped");
           delay();
     }
     ff=0;
     }
}

void delay(void)
{
     /*long double k=0;
     unsigned long int i=0;
     for (k=0;k<1000000;k++)
     {
         for (i=0;i<30;i++) ;
     }*/
     sleep(100);
}

void solve(void)
{
     int k=1,j;
     int x_=0,y_=0;
     
     for (j=0;j<10;j++)
     for (k=1;k<9;k++)
     {
         find_xy(k,&x_,&y_);
         if ( (x_!=(k-1)/3) || (y_!=(k-1)%3) )
         {
            printf("moving x[%d][%d] (k=%d)",x_,y_,k);
            //printf("\nk=%d -> pos[%d][%d] that must be = p[%d][%d] ",k,x_,y_,(k-1)/3,(k-1)%3);
            delay();//delay();//delay();
            move_tile(x_,y_,(k-1)/3,(k-1)%3);
         }
         //printf("\nk=%d -> pos[%d][%d] that must be = p[%d][%d] ",k,x_,y_,(k-1)/3,(k-1)%3);
         //delay();delay();
     }
}
