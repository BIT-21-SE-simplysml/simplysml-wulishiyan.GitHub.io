### Welcome to simplysml Pages

# this is my code. if there exist some problems, 
## Please e-mail me by s1292103908@outlook.com.

```markdown
#include<bits/stdc++.h>
using namespace std;
#define db double
const double pi = 3.1415926;
class phy_1{
	db b[7][4];
	int num[4] = {7,7,7,7};
	int k;
	public:
		phy_1(double **a, int kk = 3){
			for(int i = 0; i < 7; i++){
				for(int j = 0; j < 4; j++){
					b[i][j] = a[i][j];
				}
			}
			k = kk;
		}
		void print(){
			for(int i = 0; i < 7; i++){
				for(int j = 0; j < 4; j++){
					printf("%.2f ", b[i][j]);
				}
				printf("\n");
			}			
			return;
		}
		// 用拉依达准则(弱化版)来剔除，虽然样本数量有点少，但是只能这么将就着用啦
		void fuck_the_extreme_data(){
			double sum[4] = {0,0,0,0};
			double mu[4];
			double sigma[4] = {0,0,0,0};
			for(int i = 0; i < 7; i++){
				for(int j = 0; j < 4; j++){
					sum[j] += b[i][j];
				}
			}
			for(int i = 0; i < 4; i++){
				mu[i] = sum[i] / 7;
			}
			for(int i = 0; i < 7; i++){
				for(int j = 0; j < 4; j++){
					sigma[j] += pow(b[i][j] - mu[j], 2);
				}
			}
			for(int j = 0; j < 4; j++){
				sigma[j] /= 7;
				sigma[j] = pow(sigma[j], 0.5);
//				printf("\n%.2f  %.2f\n", sigma[j], mu[j]);
			}
			for(int i = 0; i < 7; i++){
				for(int j = 0; j < 4; j++){
					if(b[i][j] > mu[j] + 2.3 * sigma[j] || b[i][j] < mu[j] - 2.3 * sigma[j]){
						num[j]--;
						b[i][j] = 0;
					}
				}
			}
			return;
		}
		private:
			void output_the_ave_data(){
				double sum[4] = {0,0,0,0};
				for(int i = 0; i < 7; i++){
					for(int j = 0; j < 4; j++){
						sum[j] += b[i][j];
					}
				}
				cout << "Here is the average data:: ";
				for(int i = 0; i < 4; i++){
					printf("%.2f ",sum[i] / num[i]);
				}
				cout << endl;
				return;
			}
			double mu[4];
		void output_the_sigma(){
			double sum[4] = {0,0,0,0};
			double sigma[4] = {0,0,0,0};
			for(int i = 0; i < 7; i++){
				for(int j = 0; j < 4; j++){
					sum[j] += b[i][j];
				}
			}
			for(int i = 0; i < 4; i++){
				mu[i] = sum[i] / num[i];
			}
			for(int i = 0; i < 7; i++){
				for(int j = 0; j < 4; j++){
					if(b[i][j] == 0){
						continue;
					}
					sigma[j] += pow(b[i][j] - mu[j], 2);
				}
			}
			cout << "Here is the Sx data:: ";
			for(int j = 0; j < 4; j++){
				sigma[j] /= num[j];
				sigma[j] = pow(sigma[j], 0.5);
				printf("%.2e ", sigma[j]);
			}
			cout << endl;
			return;
		}
		double ans[4] = {0,0,0,0};
		void output_ua(){
			for(int i = 0; i < 7; i++){
				for(int j = 0; j < 4; j++){
					if(b[i][j] != 0){
						ans[j] += pow(b[i][j] - mu[j], 2);
					}
				}
			}
			for(int i = 0; i< 4; i++){
				ans[i] /= (num[i] - 1);
				ans[i] = pow(ans[i] , 0.5);
			}
			cout << "Here is the Ua data:: ";
			for(int j = 0; j < 4; j++){
				printf("%.2e ", ans[j]);
			}
			printf("\n");
			return;
		}
		void output_ub(){
			cout << "Here is the Ub data:: 0.03 0.03 0.03 0.03\n";
			return;
		}
		db uc[4];
		void output_uc(){
			cout << "Here is the Uc data:: ";
			for(int j = 0; j < 4; j++){
				uc[j] =  pow(pow(ans[j], 2) + pow(0.02, 2), 0.5);
				printf("%.2e ", pow(pow(ans[j], 2) + pow(0.02, 2), 0.5));
			}
			printf("\n");
		}
		public:
			void output(){
				output_the_ave_data();
				output_the_sigma();
				output_ua();
				output_ub();
				output_uc();
				printf("V= %.8e\n", pi / 4 * (mu[0] * mu[0] * mu[1] - mu[2] * mu[2] * mu[3]));
				printf("uv= %.2e\n", pi / 4 * pow( pow(2 * mu[0] * mu[1] * uc[0], 2) + pow(mu[0] * mu[0] * uc[1], 2) + pow(2 * mu[2] * mu[3] * uc[2], 2) + pow(mu[2] * mu[2] * uc[3], 2),0.5));
				cout << endl;
			}
};

int main(){
	cout << "Please Input your data on test 1:   \n";
	db** a = new double* [7];
	for(int i = 0; i < 7; i++){
		a[i] = new double[4];
	}
	for(int i = 0; i < 7; i++){
		for(int j = 0; j < 4; j++)
			cin >> a[i][j];
	}
	phy_1 p(a,2.3);
	p.fuck_the_extreme_data();
	p.output();
	for(int i = 0; i < 7; i++){
		delete[] a[i];
	}
	delete []a;
}
```
### Thanks for reading.
