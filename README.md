
/*  计算自然数e的值*/   
# include<stdio.h>  

void main()    
{    
 int i,j;   
 double e=1,single;    
 printf("Hello world!\n");   
 for(i=1;i<50;i++)   
 {   
  single=1;  
  for(j=1;j<i+1;j++)  
 {  
  ingle=single/j;  
 }  
  e+=single;  
  }  
 printf("%lf\n",e);  
  return 0;  
}   

/*****************************************************     
 用链表输入学生成绩，然后将数据排名，然后打印出来      
******************************************************/   
/*****************************************************
  用链表输入学生成绩，然后将数据排名，然后打印出来
******************************************************/
#include<stdio.h>
#include<stdlib.h>

struct student
    {
        char stuName[50];
        int  stuPoint;
        struct student * next;
    };
int main(void)
{
    int scanfNum;
    char  strTemp[50];
    struct student *stuHead=(struct student *)malloc(sizeof(struct student));
    struct student *studenti=stuHead;
    struct student *studentj;
    struct student *studentjPrev;
    int time=0;
    studenti->next=stuHead;
    struct student *stuTemp;

    while(studenti->next!=NULL)
    {

        studenti=studenti->next;
        puts("Please input a student name ");
        while (gets(studenti->stuName)==NULL||studenti->stuName[0]=='\0')
            puts("Not input a right student name, please input again");

        puts("Please input a student point");
        while( (scanfNum=scanf("%d",&studenti->stuPoint))==0 || studenti->stuPoint<0 || studenti->stuPoint>100 )
            {
                printf("Not input a right student point,please input again \n");
                gets(strTemp);                     //将错误的输入从stdin清空
            }

        studenti->next=NULL;
        printf("Press space to continue input  press q to end input \n");
        strTemp[0]=getchar();
        while(strTemp[0]!=' ' && strTemp[0]!='q' )
            {
                strTemp[0]=getchar();
            }
        if(strTemp[0]==' ')
            {
                studenti->next=(struct student *)malloc(sizeof(struct student));
                gets(strTemp);
            }
    }

    for(studenti=stuHead;studenti->next!=NULL;studenti=studenti->next)
    {
        stuTemp=studenti->next;
        puts("outer loop");
        for (studentjPrev=studenti,studentj=studenti->next; studentj!=NULL; studentjPrev=studentj,studentj=studentj->next)
        {
            puts("inter loop");
            if((studenti->stuPoint)<(studentj->stuPoint))
            {
                if(studenti->next==studentj)
                    {
                        studenti->next=studentj->next;
                        studentj->next=studenti;
                        studenti=studentj;
                        studentj=studentjPrev;
                        puts("j is next to i and i<j");
                        scanf("%s",strTemp );
                        printf("%d %d",studenti->stuPoint,studentj->stuPoint);

                    }
                else
                    {
                        studentjPrev->next=studenti;
                        studenti->next=studentj->next;
                        studentj->next=stuTemp;

                        stuTemp=studenti;
                        studenti=studentj;
                        studentj=stuTemp;
                        puts("j is not next to i and i<j");
                        scanf("%s",strTemp );
                        printf("%d %d",studenti->stuPoint,studentj->stuPoint);
                    }
            }
        }

        if (time++==0)
            stuHead=studenti;
        puts("quit from inter loop");
    }

    studenti=stuHead;
    if (studenti==NULL)
        printf("That's all!\n");
    else
        printf("All the students are below:\n");

    while(studenti!=NULL)
    {
        printf("%-20s %3d \n" ,studenti->stuName,studenti->stuPoint );
        studenti=studenti->next;
    }

    studenti=stuHead;
    while(studenti!=NULL)
    {
        free(studenti);
        studenti=studenti->next;
    }
    printf("Occupied memory %d byte has been released",time*sizeof(struct student));

    return 0;

}































