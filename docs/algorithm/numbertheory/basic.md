>记一些基础知识性质之类的，方便自己之后查看，因为oi-wiki这种，虽然内容很全，但是大部分我都不会。自己看一点记一点也好。



# 数论基础

## 整除

~~其实我有时候都不太记得整除符号那个，哪个是被除数那个是除数...~~

$a|b$ 表示，$a$ 可以整除 $b$ ，即存在 $q$ 使得 $b=aq$ 。

$b$ 是 $a$ 的倍数，$a$ 是 $b$ 的约数。

## 最大公约数

最大公约数(greatest common divisor)，简称gcd。

指两个或多个整数拥有的共同约数中最大的一个。

$a,b,c$ 的最大公约数记为 $(a,b,c)$ ，最小公倍数记为 $[a,b,c]$。

### 辗转相除法

我好像还是不会证明这个来着。。。

$gcd(a,b)=g$ ，那么 $gcd(a,b-a)=g$ 。

或者说因为后面的等于 $g$ ，所以前面的等于 $g$ ?

设 $a<b$ ,  $gcd(a,b)=g$ , $a=xg$ , $b=yg$ 。

那么 $gcd(x,y)=1$ , 所以 $gcd(x,y-x)=1$ ，额，这不还是辗转相除法吗。。。

然后这个又是咋证明的呢。。。我记得有个啥是跟互素有关的。。。

#### __gcd()

```cpp
  template<typename _EuclideanRingElement>
    _GLIBCXX20_CONSTEXPR
    _EuclideanRingElement
    __gcd(_EuclideanRingElement __m, _EuclideanRingElement __n)
    {
      while (__n != 0)
	{
	  _EuclideanRingElement __t = __m % __n;
	  __m = __n;
	  __n = __t;
	}
      return __m;
    }
```

