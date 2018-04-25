# cgv
bresenhams line drawing
#include "stdafx.h"
#include<GL/glut.h>
#include<stdio.h>
#include<math.h>
int xs,ys,xe,ye;

void init()
{
	glClearColor(1.0,1.0,1.0,1.0);
	gluOrtho2D(0,500,0,500);
}
void draw_pixel(int x,int y)
{
	glColor3f(1.0,0.0,0.0);
	glPointSize(2.0);
	glBegin(GL_POINTS);
	glVertex2i(x,y);
	glEnd();
}
void bresenham_draw_line(int x1,int x2,int y1,int y2)
{
	int dx,dy,i,P;
	int incx=1,incy=1;
	int x,y;
	dx=abs(x2-x1);
	dy=abs(y2-y1);
	if(x2<x1)
		incx=-1;
	if(y2<y1)
		incy=-1;
	x=x1;
	y=y1;
	if(dx>dy)
	{
		draw_pixel(x,y);
		P=2*dy-dx;
		for(i=0;i<dx;i++)
		{
			if(P>=0)
			{
				y+=incy;
				P+=2*(dy-dx);
			}
			else
				P+=2*dy;
			x+=incx;
			draw_pixel(x,y);
		}
	}
	else
	{
		draw_pixel(x,y);
			P=2*dx-dy;
		for(i=0;i<dy;i++)
		{
			if(P>=0)
			{
				x+=incx;
				P+=2*(dx-dy);
			}
			else
				P+=2*dx;
			y+=incy;
			draw_pixel(x,y);
		}
	}
}
void display()
{
	glClear(GL_COLOR_BUFFER_BIT);
	bresenham_draw_line(xs,xe,ys,ye);
	glFlush();
}
void main()
{
	printf("enter (x1,y1)\n");
	scanf("%d%d",&xs,&ys);
	printf("enter (x2,y2)\n");
	scanf("%d%d",&xe,&ye);
	glutInitDisplayMode(GLUT_RGB);
	glutInitWindowSize(500,500);
	glutCreateWindow("bresenhams line drawing");
	init();
	glutDisplayFunc(display);
	glutMainLoop();
}

