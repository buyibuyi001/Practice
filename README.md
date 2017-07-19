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
#include<stdio.h>
#include<math.h>
#include"Head.h"

struct student
    {
        char stuName[50];
        int  stuPoint;
        struct student * next;
    };
int main(void)
{
    int scanfNum;
    char * sc=NULL;
    struct student *stuHead=(struct student *)malloc(sizeof(struct student));
    struct student *stuCurrent=stuHead;
    stuCurrent->next=stuHead;

    puts("Ready to input information,you can end up input with enter \"quit\" \n");
    while()
    {

        stuCurrent=(struct student *)malloc(sizeof(struct student));

        puts("Please input a student name \n");
        while ((fgets(stuCurrent->stuName,50,stdin))==NULL||stuCurrent->stuName[0]=='\0')
        puts("Not input a right student name, please input again");

        puts("Please input a student point\n");
        while( (scanfNum=scanf("%d",&stuCurrent->stuPoint))==0 || stuCurrent->stuPoint<0 || stuCurrent->stuPoint>100 )  //no 0 point
            {
                printf("Not input a right student point,please input again \n");
                if (scanfNum==0)
                    *sc=getchar();
            }

        stuCurrent->next=(struct student *)malloc(sizeof(struct student));
    }




    printf("%s %d",stuCurrent->stuName,stuCurrent->stuPoint);


    stuCurrent=stuHead;
    if (stuCurrent==NULL)
        printf("That's all!\n");
    else
        printf("See information below:\n");
    while(stuCurrent!=NULL)
    {
        printf("%s %d" ,stuCurrent->stuName,stuCurrent->stuPoint );
        stuCurrent=stuCurrent->next;
    }

    stuCurrent=stuHead;
    while(stuCurrent!=NULL)
    {
        free(stuCurrent);
        stuCurrent=stuCurrent->next;
    }

    return 1;

}









