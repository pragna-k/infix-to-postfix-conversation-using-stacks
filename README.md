# infix-to-postfix-conversation-using-stacks
#include<stdio.h>

char stack[100];
int top=-1;
void push(char c)
{
   
    stack[++top]=c;
}
char pop()
{
    if (top==-1)
    {
        return -1;
    }
    else
    {
    return stack[top--];
    }
}
int priority(char k)
{
    if(k=='(')
    {
        return 0;
    }
    if (k=='+' || k=='-')
    {
        return 1;
    }
    if (k=='*' || k=='/')
    {
        return 2;
    }
    if (k=='^')
    {
        return 3;
    }
}
void main()
{
    char exp[20];
    printf("enter exp:");
    scanf("%s",exp);
    char *e;
    e=exp;
    char ch;
    while (*e!='\0')
    {
       
        if (isalnum(*e))
        {
            printf("%c",*e);
        }
        else if (*e=='(')
        {
            push(*e);
        }
        else if (*e==')')
        {
            while ((ch=pop())!='(')
            {
                printf("%c",ch);
            }
        }
        else
        {
            while (priority(stack[top])>=priority(*e))
            {
                printf("%c",pop());
            }
            push(*e);
        }
        e++;
    }
    while (top!=-1)
    {
        printf("%c",pop());
    }
}
output:
enter exp:(a+b)*c+(d-a)
ab+c*da-+
