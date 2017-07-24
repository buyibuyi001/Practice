

/*****************************************************     
 用链表输入学生成绩，然后将数据排名，然后打印出来      
******************************************************/   
/*****************************************************
  用链表输入学生成绩，然后将数据排名，然后打印出来
******************************************************/
/*****************************************************
  用链表方式输入学生成绩，然后将数据排名，然后打印出来
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
    int    scanfNum;
    int    time=0;
    char   strTemp[50];
    struct student *stuHead=(struct student *)malloc(sizeof(struct student));
    struct student *studenti;
    struct student *studentj;
    struct student *studentjPrev;
    struct student *stuTemp=(struct student *)malloc(sizeof(struct student));;
    struct student *stuTemp1;

    studenti=stuHead;
    while(studenti!=NULL)
    {
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
        studenti=studenti->next;
    }

    studenti=stuHead;
    while(studenti!=NULL)
    {
        printf(" %p \n" ,studenti );
        studenti=studenti->next;
    }

    for(studenti=stuHead;studenti->next!=NULL;studenti=studenti->next)
    {
        puts("i loop start");
        for (studentjPrev=studenti,studentj=studenti->next; studentj!=NULL; studentjPrev=studentj,studentj=studentj->next)
        {
            printf("j loop start i,j is %d %d   \n",studenti->stuPoint,studentj->stuPoint);
            if((studenti->stuPoint)<(studentj->stuPoint))
            {

                if(studentj->next==NULL)
                    {

                        studentj->next=(struct student *)malloc(sizeof(struct student));
                        studentj->next=studenti->next;
                        studenti->next=NULL;
                    }

                if(studenti->next==studentj)
                    {
                        studenti->next=studentj->next;
                        studentj->next=studenti;
                        studenti=studentj;
                        studentj=studentjPrev;
                        printf("j is next to i\n");
                    }
                else
                    {
                        stuTemp=studenti->next;
                        studentjPrev->next=studenti;
                        studenti->next=studentj->next;
                        studentj->next=stuTemp;

                        stuTemp=studenti;
                        studenti=studentj;
                        studentj=stuTemp;
                        printf("j is not next to i\n");
                    }
            }
            printf("after changing,");
            printf("i,inext,j,jnextaddress is%d %d %d %p\n\n",studenti->stuPoint,studenti->next->stuPoint,studentj->stuPoint,studentj->next);
            scanf("%c",strTemp);
        }
        puts("j loop end \n");

        if (time++==0)
            {
                stuHead=studenti;
                stuTemp1=stuHead;
            }
        else
                stuTemp1->next=studenti;
                stuTemp1=stuTemp1->next;
    }

    if (stuHead==NULL)
        printf("That's all!\n");
    else
        printf("All the students are below:\n");

    studenti=stuHead;
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










































