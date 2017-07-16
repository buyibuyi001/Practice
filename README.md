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
        	single=single/j;
        }
        e+=single;
    }
    printf("%lf\n",e);
    return 0;
}
