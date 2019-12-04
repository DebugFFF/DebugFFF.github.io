# C语言

## 文件操作

常见函数：

```C
//打开文件
FILE * fopen(const char *filename，const char * mode);
//
int fgetc ( FILE * stream );
//
int fputc ( int character, FILE * stream );
//
int fclose(FILE * stream);
//
int fprintf ( FILE * stream, const char * format, ... );
//
int fscanf ( FILE * stream, const char * format, ... );
//
char * fgets ( char * str, int num, FILE * stream );
//
void fputs( char * str, FILE * stream );
//将流的位置设置为开头
void rewind ( FILE * stream );
//重新定位位置,offset偏移量(正数负数和0,字节),origin表示起点(SEEK_SET,SEEK_CUR,SEEK_END)
int fseek ( FILE * stream, long int offset, int origin );
//获取当前位置,距离文件开始处的字节数，第一个字节处是0
long int ftell ( FILE * stream );
//显式刷新流缓冲区
int fflush(FILE * stream);
//获取当前位置
int fgetpos ( FILE * stream, fpos_t * pos );
//重新定位位置
int fsetpos ( FILE * stream, const fpos_t * pos );
//检查文件结束标志
int feof ( FILE * stream );
//检查错误标志
int ferror ( FILE * stream );
//从流中取消字符
int ungetc ( int character, FILE * stream );
//指定缓冲区的模式和大小（以字节为单位）
int setvbuf ( FILE * stream, char * buffer, int mode, size_t size );
//ptr是读入文件数据的内存存储地址，size数据块大小，count数据块的数目，stream文件指针
size_t fread ( void * ptr, size_t size, size_t count, FILE * stream );
//ptr要写入的数据块，size数据块大小，count数据块的数目，stream文件指针
size_t fwrite ( const void * ptr, size_t size, size_t count, FILE * stream );
```

| 标识 | 说明                                                         |
| ---- | ------------------------------------------------------------ |
| "r"  | 读取：打开文件进行输入操作。文件必须存在。                   |
| "w"  | 写：创建一个空文件用于输出操作。如果已经存在同名文件，则将其内容丢弃，并将该文件视为**新的空文件**。 |
| "a"  | 追加：打开文件以在文件末尾输出。输出操作始终将数据写入文件的末尾，然后进行扩展。重新定位操作（fseek，fsetpos，rewind）将被忽略。如果文件不存在，则创建该文件。 |
| "r+" | 读取/更新：打开文件进行更新（用于输入和输出）。该文件必须存在。 |
| "w+" | 写入/更新：创建一个**空文件**并打开以进行更新（用于输入和输出）。如果同名文件已经存在，则将其内容丢弃，并将该文件视为新的空文件。 |
| "a+" | 追加/ 更新：打开文件进行更新（用于输入和输出），所有输出操作均在文件末尾写入数据。重新定位操作（fseek，fsetpos，rewind）会影响下一个输入操作，但输出操作会将位置移回文件末尾。如果文件不存在，则创建该文件。 |



## 将结构体数据存入和读取

### fwrite和fread

>//ptr是读入文件数据的内存存储地址，size数据块大小，count数据块的数目，stream文件指针
>`size_t fread ( void * ptr, size_t size, size_t count, FILE * stream );`  数据、大小、数量、指针
>//ptr要写入的数据块，size数据块大小，count数据块的数目，stream文件指针
>`size_t fwrite ( const void * ptr, size_t size, size_t count, FILE * stream );`

```C
typedef struct student
{
	char no[13];
	char name[10];
	char sex[4];
}s[3],r[3];   //学生结构体
void jianli(int n) 
{
	int i,a,b;FILE * pf;
	if((pf=fopen("D:\\a.dat","a+"))==NULL) return ;
	input(s);

	for(i=0;i<3;i++)
	{
		fwrite(&s[i],sizeof(student),1,pf);
	}

	for(i=0;i<3;i++)
	{
		fread(&r[i],sizeof(student),1,pf);
	}
	fclose(pf);

}
```

### sprintf和