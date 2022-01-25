[***目录***]()
[1. 程序断言：用来调试代码是否满足条件](#程序断言：用来调试代码是否满足条件)
[2.  获取指定地址上的一个字节或字 ](#获取指定地址上的一个字节或字 )
[ 3.计算最大值和最小值 ](#计算最大值和最小值 )
[4. 将一个字母转换为大写](#将一个字母转换为大写 )
[5. 获取数组元素的个数](#获取数组元素的个数 )
[6. 颜色转换 ](#颜色转换  )
[7. 二进制字符串转换为十进制整数 ](#二进制字符串转换为十进制整数  )
[8. 把二进制字符串转换为十进制](#把二进制字符串转换为十进制)
[9.将十进制转换为八进制 ](#将十进制转换为八进制  )
[10. 十进制转二进制 ](#十进制转二进制  )
[11. 十六进制转十进制](#十六进制转十进制 )
[12. 八进制转十进制 ](#八进制转十进制 )
[13. RAM计算前导零指令（__clz）使用C语言编写 ](#ram计算前导零指令clz使用c语言编写  )
[14. 获取一个字的高位和低位字节](#获取一个字的高位和低位字节 )
[15. 从一个结构的成员指针找到其容器的指针  ](#从一个结构的成员指针找到其容器的指针   )
[16. 获取按指定宽度对齐的向下数 ](#获取按指定宽度对齐的向下数  )
[17. 获取按指定宽度对齐的向上数 ](#获取按指定宽度对齐的向上数  )


## 1. 程序断言：用来调试代码是否满足条件
 ```c
 #define

FILE_ASSERT(term)

do

{

   if (!(term))

{

       printf("Assert failed. Condition(%s). [%s][%d]\r\n",

term, __FUNCTION__, __LINE__);                 \

while(1)                                                         {                                                                ;                                                       }

   }

} while (0) 
 ```
 
## 2.  获取指定地址上的一个字节或字 
```c
#define SITE_B( x ) ( *( (byte *) (x) ) )

#define SITE _W( x ) ( *( (word *) (x) ) ) 
```
## 3.计算最大值和最小值 
```c
#define LV_MAX( x, y ) ( ((x) > (y)) ? (x) : (y) )

#define LV_MIN( x, y ) ( ((x) < (y)) ? (x) : (y) ) 
```
## 4. 将一个字母转换为大写 
```c
#define CAPITAL( c ) ( ((c) >= 'a' && (c) <= 'z') ? ((c) - 0x20) : (c) ) 
```
## 5. 获取数组元素的个数
```c
#define MY_SIZE( x ) ( sizeof( (x) ) / sizeof( (x[0]) ) ) 
```
## 6. 颜色转换 
```c
#define RGB888_turn_monochrome(color)        ((color)?0:1)


#define RGB888_turn_RGB233(color)            ((((color&0xff0000)>>22) << 6) +

                                                   (((color&0xff00)>>13) << 3) +

(((color&0xff)>>5)))


#define RGB888_turn_RGB565(color)             ((((color&0xff0000)>>19) << 11) +

                                                   (((color&0xff00)>>10) << 5) +

(((color&0xff)>>3)))


int LV_RGB888(uint32_t color)

{

   int ret=0;

 switch(cfgColorDepth)

 {

 case 1: // 颜色深度1，单色

 {

       ret= RGB888_turn_monochrome(color);

 break;

 }

 case 8: // 颜色深度8，RGB233

 {

       ret= RGB888_turn_RGB233(color);

 break;

 }

 case 16: // 颜色深度16，RGB565

 {

       ret= RGB888_turn_RGB565(color);

 break;

 }

 case 24: // 颜色深度24，RGB888

 {

       ret= color;

 break;

 }

 default:

 break;

 }

 return ret;

} 
```
## 7. 二进制字符串转换为十进制整数 
```c
/**

* @brief       二进制字符串转换为十进制整数

* @param       str：待反转的字符串

* @retval      反转字符串

*/

static void lv_atk_bit_str_reverse(char str[])

{

 int n=strlen(str);

 int i;

 char temp;


 for (i = 0;i < (n/2); i++)

 {

       temp = str[i];

       str[i] = str[n-i-1];

       str[n-i-1] = temp;

 }

} 
```
## 8. 把二进制字符串转换为十进制
```c
/**

* @brief       把二进制字符串转换为十进制

* @param       pbin：二进制

* @retval      二进制字符串转换为十进制整数的结果

*/

static long lv_atk_bit_bin_to_dec(const char *pbin)

{

 int ii=0;

 long result=0;


 while (pbin[ii] != 0)

 {

       result = result * 2 + (pbin[ii] - '0');

       ii++;

 }


 return result;

}
```
## 9.将十进制转换为八进制 
```c
/**

* @brief       将十进制转换为八进制

* @param       n：十进制

* @retval      返回八进制

*/

long lv_atk_dec_to_oct(long dec)

{

 int oct = 0, i = 0;


   i = 1;


 while (dec != 0)

 {

       oct += (dec % 8) * i;

       dec /= 8;

       i *= 10;

 }


 return oct;

} 
```
## 10. 十进制转二进制 
```c
/**

* @brief       十进制转二进制

* @param       n：十进制

* @retval      返回二进制

*/

long lv_atk_bec_to_bin(long n)

{


 long result=0,k=1,i,temp;

   temp = n;


 while(temp)

 {

       i = temp%2;

       result = k * i + result;

       k = k*10;

       temp = temp/2;

 }

   printf("%ld\n", result);


 return result;

} 
```
## 11. 十六进制转十进制
```c
/**

* @brief       十六进制转十进制

* @param       n：十六进制

* @retval      返回十进制

*/

long lv_atk_hex_to_dex(char*s)

{

 int i,t;

 long sum=0;


 for(i=0;s[i];i++)

 {

 if(s[i]>= '0'  &&s[i]<='9')/* 当字符是'0'--'9'时，*-‘0'就行了 */

 {

           t=s[i]-'0';

 }


 if(s[i]>='a'&&s[i]<='z')

 {

           t=s[i]-'a'+10;/* 当字符是 abcdef 时，*-‘a’+10 就行了 */

 }


 if(s[i]>='A'&&s[i]<='Z')

 {

           t=s[i]-'A'+10;/* 当字符是 ABCDEF 时，*-‘A’+10 就行了 */

 }


       sum=sum*16+t;

 }


 return sum;

} 
```
## 12. 八进制转十进制 
```c
/**

* @brief       八进制转十进制

* @param       n：八进制的数值

* @retval      返回十进制

*/

long lv_atk_oct_to_dex(long n)

{

 int i=0,tmp,sum=0;


 while(n)

 {

       tmp=n%10;

       n=n/10;

       sum+=tmp*pow(8,i);

       i++;

 }


   printf("%d",sum);


 return sum;

}
```
## 13. RAM计算前导零指令clz使用C语言编写 
```c
int lv_clz(unsigned int  app_readly_list[])

{

 int bit = 0;


 for (int i = 0; i < 32; i++)

 {

 if (app_readly_list[i] == 1)

 {

 break;

 }


       bit ++ ;

 }


 return bit;

} 
```
## 14. 获取一个字的高位和低位字节 
```c
#define VALUE_L(x) ((byte) ((word)(x) & 255))

#define VALUE_H(x) ((byte) ((word)(x) >> 8))
```
## 15. 从一个结构的成员指针找到其容器的指针  
```c
#define os_container_of(ptr, type, member)      \

   ((type *)((char *)(ptr) - (unsigned long)(&((type *)0)->member))) 
```
## 16. 获取按指定宽度对齐的向下数 
```c
#define ALIGN_DOWN(size, align)      ((size) & ~((align) - 1)) 
```
## 17. 获取按指定宽度对齐的向上数
```c
#define ALIGN_UP(size, align)        (((size) + (align) - 1) & ~((align) - 1)) 
```
