

/*****************************************************   
  用链表方式输入学生成绩，然后将数据排名，然后打印出来
******************************************************/   
#include<stdio.h>   
#include<stdlib.h>   

struct student    
    {
        char name[50];   
        int  point;   
        struct student * next;   
    };    
int main(void)   
{   
    struct student *stuHead=(struct student *)malloc(sizeof(struct student));   
    struct student *studenti;   
    struct student *studentj;   
    struct student *studentiNext;   
    struct student *studentjPrev;   
    struct student *stuNode;   
    int    time=0;   
    char   strTemp[50];   

    for(studenti=stuHead ; studenti!=NULL ;  studenti=studenti->next )   
    {   
        puts("Please input a student name ");   
        while (gets(studenti->name)==NULL||studenti->name[0]=='\0')   
            puts("Not input a right student name, please input again");   

        puts("Please input a student point");   
        while( scanf("%d",&studenti->point)==0   
            || studenti->point<0 || studenti->point>100 )   
            {   
                printf("Not input a right student point,please input again \n");   
                gets(strTemp);                     //将错误的输入从stdin清空  
            }

        studenti->next=NULL;

        printf("Press space to continue input  press q to end input \n");
        strTemp[1]=getchar();
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

    for(studenti=stuHead ; studenti->next!=NULL ; studenti=studenti->next)
    {
        studentjPrev=studenti;
        for (studentj=studenti->next; studentj!=NULL;
            studentjPrev=studentj,studentj=studentj->next)
            {
                printf("jloop starti,j %d %d\n",studenti->point,studentj->point);
                if(studenti->point<studentj->point)
                    {
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
                                studentiNext=studenti->next;
                                studentjPrev->next=studenti;
                                studenti->next=studentj->next;
                                studentj->next=studentiNext;

                                studentiNext=studenti;
                                studenti=studentj;
                                studentj=studentiNext;
                                printf("j is not next to i\n");
                            }
                    }
            printf("jloop end,i and j is %d %d",studenti->point,studentj->point);
            scanf("%c",strTemp);
        }

        if (time++==0)    // redefine the stuhead
            {
                stuHead=studenti;
                stuNode=stuHead;
            }
        else
            {
                stuNode->next=studenti;
                stuNode=stuNode->next;
            }
    }

    if (stuHead==NULL)
        printf("That's all!\n");
    else
        printf("All the students are below:\n");

    studenti=stuHead;
    while(studenti!=NULL)
    {
        printf("%-20s %3d \n" ,studenti->name,studenti->point );
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





















































