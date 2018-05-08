# blur-assermble-in-gray-change
fuzzy function is S
#include<opencv2/opencv.hpp>
#include<iostream>
using namespace cv;
using namespace std;
int fuzzyS(int p, int a, int b, int c);
int main()
{
	
	Mat I = imread("C:\\Users\\64166\\Pictures\\Saved Pictures\\kapu.jpg",0);
	
	
	{
		for (int i = 0; i < I.rows; i++)
		{
			uchar *p = I.ptr(i);
			for (int j = 0; j < I.cols; j++)
			{
				int ud = fuzzyS(p[j], 0, 30, 90);
				int ug = fuzzyS(p[j], 60, 90, 150);
				int ub = fuzzyS(p[j], 120, 150, 255);

				p[j] = (ud * 0 + ug * 127 + ud * 255) / (ud + ug + ub);
			}
		}

	}
	
	imshow("ojbk", I);
	waitKey();

}
int fuzzyS(int p,int a, int b, int c)
{
	
			if (p < a)
				p = 0;
			else
				if (a< p < b)
					p = 2 * ((p - a) / (c-a)) ^ 2;
				else
					if (b <= p <= c)
						p = 1 - (2 * (p - c) / (c-a)) ^ 2;
					else
						p = 1;


		

	
	return p;

}
