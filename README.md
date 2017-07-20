# include<stdio.h>
=
-
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
        	single=single/j;
        }
        e+=single;
    }
    printf("%lf\n",e);
    return 0;
}

/*****************************************************

******************************************************/
/*****************************************************
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
    struct student *stuCurrent=stuHead;
    stuCurrent->next=stuHead;

    puts("Ready to input information,you can end up input with enter quit");
    while(stuCurrent->next!=NULL)
    {

        stuCurrent=stuCurrent->next;
        puts("Please input a student name ");
        while (gets(stuCurrent->stuName)==NULL||stuCurrent->stuName[0]=='\0')
            puts("Not input a right student name, please input again");

        puts("Please input a student point");
        while( (scanfNum=scanf("%d",&stuCurrent->stuPoint))==0 || stuCurrent->stuPoint<0 || stuCurrent->stuPoint>100 )
            {
                printf("Not input a right student point,please input again \n");
                gets(strTemp);                     //将错误的输入从stdin清空
            }

        stuCurrent->next=NULL;

        printf("Press space to continue input  press q to end input \n");
        strTemp[0]=getchar();
        while(strTemp[0]!=' ' && strTemp[0]!='q' )
            {
                strTemp[0]=getchar();
            }

            // { printf("good job %d"   ,scanf("%s",strTemp));  break;}
        if(strTemp[0]==' ')
            {
                stuCurrent->next=(struct student *)malloc(sizeof(struct student));
                gets(strTemp);
            }

    }

    stuCurrent=stuHead;
    if (stuCurrent==NULL)
        printf("That's all!\n");
    else
        printf("All the students are below:\n");

    while(stuCurrent!=NULL)
    {
        printf("%-20s %3d \n" ,stuCurrent->stuName,stuCurrent->stuPoint );
        stuCurrent=stuCurrent->next;
    }

    stuCurrent=stuHead;
    while(stuCurrent!=NULL)
    {
        free(stuCurrent);
        stuCurrent=stuCurrent->next;
    }
    printf("Memory has been released");

    return 0;

}




















