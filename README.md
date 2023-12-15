yêu cầu 1
 
 #include <stdio.h>
#include <conio.h>
#include <stdlib.h>
int main()
{
	FILE * fp;
	char filename[67], ch;
		printf("FILENAME: ");
		gets(filename);
	if ((fp = fopen (filename, "w")) == NULL ) //mo tap tin de ghi
	{
		printf("Create file error \n");
		exit(1);
	}
while (( ch = getche() ) != '\r') //ghi den khi an enter
	putc( ch, fp);
fclose(fp);
return 0;
} 







 yêu cầu 2
#include <stdio.h>
#include <conio.h>
#include <stdlib.h>
int main()
{
	FILE * fp;
	char filename[67], ch;
		printf("FILENAME: ");
		gets(filename);
	if ((fp = fopen (filename, "r")) == NULL ) //mo tap tin de ghi
	{
		printf("Open file error \n");
		exit(1);
	}
while ((ch =  getc(fp)) != EOF ) // doc den khi het tap tin
	printf("%c",ch);
fclose(fp);
return 0;
}







yêu cầu 3 

#include <stdio.h>
#include <stdlib.h>
int main()
{
  int a[3][3]={{1,2,3},{4,5,6},{7,8,9}};
  int m=3;
   FILE * fp;
   char path[50];

   printf("\n Nhap duong dan: ");
   fflush(stdin);
   gets(path);

    fp = fopen(path,"wt");
     if(fp == NULL)
     {
     	 printf("\n Loi mo file ");
     	 exit(0);
     }
  else 
  {
  	fprintf(fp,"So dong, cot la %d \n", m);
  	for(int i=0; i<m; i++)
  	{
  		for(int j=0; j<m; j++) //ghi dong
  		{
  			fprintf(fp, "%3d", a[i][j]); 
  		}
  	fprintf(fp,"\n");
  	}
  	fclose(fp);
  }
}



 yêu cầu 4 

 #include <stdio.h>
#include <conio.h>
#include <string.h>

typedef struct
{
	char Ma[10];
	char HoTen[40];
}SinhVien;

void ReadFile(char *FileName);
void WriteFile(char *FileName);
void Search(char *FileName);
   int main()
   {
   	 int c;
   	 for(;;)
   	 {
   	 	printf("\n \t*_*_*_*_*_*_*_*_*_*_*_*_*\n");
   	 	printf("\t 1. Nhap DSSV\n");
   	 	printf("\t 2. In DSSV\n");
   	 	printf("\t 3. TimKiem\n");
   	 	printf("\t 4. Thoat\n");
   	 	printf("\t Ban chon 1,2,3,4 : ");
   	 	scanf("%d",&c);
   	 	fflush(stdin);
   	 	if (c==1)
   	 	{
   	 		 WriteFile("SinhVien.txt");
   	 	}
		else if(c==2)
		{ 
		     ReadFile("SinhVien.txt");
		}
		else if(c==3)
		{
			 Search("SinhVien.txt");		 
        }
		else break;
	}
	
}		 
  void WriteFile(char *FileName)
   {
   	 FILE *f;
   	 int n,i;
   	 SinhVien sv;
   	 f=fopen(FileName,"ab");
   	 printf("Nhap vao so luong sinh vien ");
   	 scanf("%d",&n);
   	 for(i=0;i<n;i++)
   	 {
   	 	printf("Sinh vien thu %i\n",i);
   	 	fflush(stdin);
   	 	printf("-MSVV: ");
   	 	gets(sv.Ma);
   	 	printf(" -Hoten: ");
   	 	gets(sv.HoTen);
   	 	fwrite(&sv,sizeof(sv),1,f);
   	 	}
   	 	fclose(f);
   	 	printf(" Bam ban phi bat ky de tiep tuc ");
   	 	getch();
   	}
	   void ReadFile(char *FileName)
{
	FILE * f;
	SinhVien sv;
	f = fopen(FileName, "rb");
	printf(" MSSV | Ho va ten\n");
	fread(&sv,sizeof(sv), 1, f);
	while(!feof(f))
	{
		printf("%s | %s\n", sv.Ma,sv.HoTen);
		fread(&sv,sizeof(sv),1,f);
	}
	fclose(f);
	printf("Bam phim bat ky de tiep tuc!!!");
	getch();
} 	
   	 void Search(char *FileName)
   	 {
		char MSSV[10];
		FILE *f;
		int Found=0;
		SinhVien sv;
		fflush(stdin);
		printf(" Ma so sinh vien can tim: ");
		gets(MSSV);
		f=fopen(FileName,"rb");
		while (!feof(f) &&  Found==0)
		{
		  fread(&sv,sizeof(sv),1,f);
		  if (strcmp(sv.Ma,MSSV)==0)
		      Found=1;
		 }
		 fclose(f);
		 if (Found == 1)
		 {
		    printf("Tim thay sinh vien co ma %s. Ho ten la : %s ",sv.Ma,sv.HoTen);
		 }
		 else
		 {
		 	printf("Tim khong thay sinh vien co ma: %s",MSSV);
		 }
		 printf("\n Bam phim bat k? de tiep tuc !!!");
		 getch();
	}




 yêu cầu 5
   #include <stdio.h>

void nhapMang(int arr[], int n) {
    printf("Nhap mang %d so nguyen duong:\n", n);
    for (int i = 0; i < n; ++i) {
        do {
            printf("Nhap phan tu thu %d: ", i + 1);
            scanf("%d", &arr[i]);
        } while (arr[i] <= 0); // Ðam bao nhap so nguyên duong
    }
}

void ghiFile(const char* path, int arr[], int n) {
    FILE* outFile = fopen(path, "w");
    if (outFile != NULL) {
        for (int i = 0; i < n; ++i) {
            fprintf(outFile, "%d ", arr[i]);
        }
        fclose(outFile);
        printf("Ghi mang vao file thanh cong.\n");
    } else {
        fprintf(stderr, "Khong the mo file de ghi.\n");
    }
}

void thucHienYeuCau(const char* inputPath, const char* outputPath) {
    const int MAX_SIZE = 100;
    int mang[MAX_SIZE];
    int n;

    printf("Nhap so luong phan tu cua mang: ");
    scanf("%d", &n);

    nhapMang(mang, n);
    ghiFile(inputPath, mang, n);

    // Tính tong
    int tong = 0;
    for (int i = 0; i < n; ++i) {
        tong += mang[i];
    }

    // Tìm max và min
    int max = mang[0], min = mang[0];
    for (int i = 1; i < n; ++i) {
        if (mang[i] > max) {
            max = mang[i];
        }
        if (mang[i] < min) {
            min = mang[i];
        }
    }

    // Ghi ket qua vào file
    FILE* resultFile = fopen(outputPath, "w");
    if (resultFile != NULL) {
        fprintf(resultFile, "Tong: %d\n", tong);
        fprintf(resultFile, "Max: %d\n", max);
        fprintf(resultFile, "Min: %d\n", min);
        fclose(resultFile);
        printf("Ghi ket qua vao file thanh cong.\n");
    } else {
        fprintf(stderr, "Khong the mo file de ghi ket qua.\n");
    }

    // Ðoc noi dung file và hien thi lên màn hình
    FILE* resultFileRead = fopen(outputPath, "r");
    if (resultFileRead != NULL) {
        printf("Noi dung file ket qua:\n");
        char line[100];
        while (fgets(line, sizeof(line), resultFileRead)) {
            printf("%s", line);
        }
        fclose(resultFileRead);
    } else {
        fprintf(stderr, "Khong the mo file de doc ket qua.\n");
    }
}

int main() {
    const char* inputPath = "input.txt";
    const char* outputPath = "output.txt";

    thucHienYeuCau(inputPath, outputPath);

    return 0;
}

