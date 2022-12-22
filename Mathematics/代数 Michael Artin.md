# 代数 Michael Artin

## Chap. 2. 群

### 1. 合成法则

**Def 2-1-1. 合成法则：**一个有两个变量的函数或映射：$$S\times S\rightarrow S$$，此处$S\times S$表示集合的积集，其元素为集合$S$中的元素对

**Def 2-1-2. 合成法则的结合律：**$(ab)c=a(bc)$

**Def 2-1-3. 合成法则的交换律：**$ab=ba$

结合律比交换律更基础，e.g.函数的复合

**Lemma 2-1-1. **令集合$S$上的合成法则满足结合律，则有且仅有一种方式定义$S$中任意$n$个元素满足以下性质的乘积，记作$[a_1a_2\cdots a_n]$：

1. $[a_1]=a_1$
2. $[a_1a_2]$由合成法则给出
3. $\forall n \in \Z_+, [a_1a_2 \cdots a_ia_{i+1} \cdots a_n] = [a_1a_2\cdots a_i][a_{i+1}\cdots a_n]$

> **Pf. **对$n$用数学归纳法

**Def 2-1-4. 合成法则的恒等元：**集合$S$中的元素$e$，若$\forall a \in S,ea=ae=a$

**Def 2-1-5. 可逆：**若在$S$上定义了一个满足结合律且有恒等元$1$的合成法则，并记作乘法。那么$a\in S$可逆，若$\exists b \in S,ab=1 \and ba=1$，其中$b$称为$a$的逆，记作$a^{-1}$或$-a$

**Lemma 2-1-2. 逆的性质：**

1. 如果$a$存在左逆$l$和右逆$r$，即$la=ar=1$，那么$l=r=a^{-1}$
2. 如果$a$可逆，则其逆唯一
3. $(ab)^{-1}=b^{-1}a^{-1}$
4. 尽管$a$不可逆，$a$也可以有左逆或右逆

### 2. 群、子群

**Def 2-2-1. 群：**一个群是一个带有满足以下性质的合成法则的集合$G$：

1. $\forall a,b,c \in G,(ab)c=a(bc)$
2. $1\in G:\forall a \in G,1a=a1=a$
3. $\forall a \in G, \exists b,ab=ba=1$

**Def 2-2-2. 阿贝尔群：**合成法则满足结合律的群

**Def 2-2-3. 群的阶：**群$G$的阶是其包含的元素个数，记作$\left|G\right|$

> 一些记号：
>
> $\Z^+$：整数加群
>
> $\R^+$：实数加群
>
> $\R^{\times}$：实数乘法群，其集合为非$0$实数
>
> $\C^+,\C^\times$：复数加群和复数乘法群

**Lemma 2-2-1. 消去律：**令$a,b,c\in G$，群$G$的合成法则用乘法表示。若$ab=ac \or ba=bc$，则$b=c$

**Def 2-2-4. $n\times n$一般线性群：**所有$n\times n$可逆矩阵组成的群，记作$GL_n$

**Def 2-2-5. 对称群：**指标集合$\{1,2,\cdots,n\}$的置换群，记作$S_n$，其阶为$n!$

**Def 2-2-6. 子群：**群$G$的子集$H$称为一个子群，如果其满足以下性质：

1. 封闭性：若$a \in H \and b \in H$，则$ab \in H$
2. 恒等元：$1 \in H$
3. 逆元：若$a \in H$，则$a^{-1}\in H$

**Def 2-2-7. 圆群：**$\C^\times$中绝对值为1的复数的子集

**Def 2-2-8. 特殊线性群：**$GL_n$中所有行列式为1的矩阵的子集，记作$SL_n$

### 3. $\Z^+$的子群

**Th 2-3-1. **若$S$为$\Z^+$的子群，则$S$或为平凡子群$\{0\}$，或是有形式$\Z a$，其中$a$为$S$中最小正整数

> **Pf. **寻找双向的子集关系，即$\Z a \sub S\and S\sub \Z a$

**Def 2-3-1. 生成子群：**由$a$与$b$生成的子群$S = \Z a + \Z b$

**Def 2-3-2. 最大公因数：**由**Th 2-3-1**，$\exists d \in \Z_+,\Z a + \Z b = \Z d$，$d$称为$a$与$b$的最大公因数，记作$gcd(a,b)$

**Lemma 2-3-1. **设$a,b$为不全为$0$的整数，设$d=gcd(a,b)$，则：

1. $d\mid a,d\mid b$
2. 若$e\mid a \and e\mid b$，$e\mid d$
3. $\exists r,s \in \Z,d=ra+sb$

**Def 2-3-3. 互素：**$a$与$b$互素当且仅当$gcd(a,b)=1$

**Ch 2-3-1. **$a$与$b$互素当且仅当$\exists r,s \in \Z,ra+sb=1$

**Ch 2-3-2. **令$p$为一个素整数，若$p\mid ab$，则$p\mid a \or p\mid b$

**Def 2-3-4. 最小公倍数：**由**Th 2-3-1**，$\exists m \in \Z_+,\Z a \cap \Z b = \Z m$，$m$称为$a$与$b$的最小公倍数，记作$lcm(a,b)$

**Lemma 2-3-2. **设$a,b\in \Z \setminus \{0\}$，$m = lcm(a,b)$，则

1. $a\mid m,b\mid m$
2. 若$a\mid n \and b \mid n$，则$m\mid n$

**Ch 2-3-3. **$gcd(a,b)\times lcm(a,b) = ab$

### 4. 循环群

**Def 2-4-1. 循环子群：**由一元素$x \in G$生成的循环子群$H$是$x$的所有幂的元素的集合。它是$G$中包含$x$的最小子群，经常记作$\langle x\rangle$

**Lemma 2-4-1. **令$\langle x \rangle$是群$G$的由$x$生成的循环子群，且令$S$表示满足$x^k=1$的整数$k$的集合，则：

1. 集合$S$是$\Z^+$的子群
2. $x^r=x^s\and r \ge s \iff x^{r-s}=1 \iff r -s\in S$
3. 若$S$为非平凡子群，$\exists n \in \Z_+,S=\Z n$，幂$1,x,x^2,\cdots ,x^{n-1}$是$\langle x \rangle$中不同的元素，且$\langle x \rangle$的阶为$n$

> **Pf. **
>
> 1. $x^k=x^l=1 \iff x^{k+l}=x^kx^l=1$，即$k,l \in S \iff k+l \in S$
>
>    $x^0=1\iff 0 \in S$
>
>    $k \in S \iff x^k = S \iff x^{-k} = (x^{k})^{-1} = 1^{-1}=1 \iff -k\in S$
>
> 2. 由**Lemma 2-2-1**得
>
> 3. 由于$S$是非平凡的，由**Th 2-3-1**得，$\exists n \in \Z_+,S=\Z n$，且$n$为$S$中最小正整数
>
>    $\forall k \in \Z_+,\exists q \in \Z,r\in \Z_+\cap[0,n),s.t.k=qn+r\implies x^k=x^{qn}x^r=x^r \in \{1,x,x^2,\cdots,x^{n-1}\}$

**Def 2-4-2. $n$阶循环群：** **Lemma 2-4-1.3**中描述的$\lang x \rang$称为$n$阶循环群

**Def 2-4-3. 元素的阶：**群中的一个元素有阶$n$，若$n$为满足$x^n=1$的最小正整数，事实上，$n=\left| \lang x \rang \right|$

**Lemma 2-4-2. **在任何群中，恒等元是唯一阶为$1$的元素

**Def 2-4-4. 无限阶：**若不存在$n \in \Z_+$满足$x^n=1$，则称$x$是无限阶的，$\lang x\rang$为无限循环群

**Lemma 2-4-3. **若$x$为群中阶为$n$的元素，$k=qn+r \in \Z$，其中$q \in \Z,r\in \Z_+\cap[0,n)$，则：

1. $x^k = x^r$
2. $x^k=1 \iff r = 0$
3. $x^k$的阶为$\frac{n}{gcd(k,n)}$

**Def 2-4-5. 群$G$中由子集$H$生成的子群：**$G$中包含$H$的最小的子群，若$H$生成的群为$G$，则称$H$**生成**$G$

**Def 2-4-6. 克莱因四元群：**由形如$\begin{bmatrix} & \pm1\\ \pm1 & \end{bmatrix}$的矩阵构成的最小的非循环群

**Def 2-4-7. 四元数群：**$H=\{\pm1,\pm i,\pm j, \pm k\}$，其中：$1=\begin{bmatrix}1&0\\0&1\end{bmatrix},i=\begin{bmatrix}i&0\\0&i\end{bmatrix},j=\begin{bmatrix}0&1\\-1&0\end{bmatrix},k=\begin{bmatrix}0&i\\-i&0\end{bmatrix}$

### 5.同态

**Def 2-5-1. 群同态：**若$G$和$G'$是两个用乘法记号表示的群，一个同态$\varphi: G\rarr G'$是一个从$G$到$G'$的映射，满足$\forall a,b\in G, \varphi(ab)=\varphi(a)\varphi(b)$

**Def 2-5-2. 平凡同态：**将$G$中的每一个元素映射为$G'$中的恒等元

**Lemma 2-5-1. **令$\varphi:G\rarr G'$是群同态，则：

1. $\forall a_1,a_2,\cdots,a_k \in G,\varphi(a_1a_2\cdots a_k)=\varphi(a_1)\varphi(a_2)\cdots\varphi(a_k)$
2. $\varphi(1_G)=1_{G'}$
3. $\varphi(a^{-1})=\varphi(a)^{-1}$

**Def 2-5-3. 像：**同态$\varphi:G\rarr G'$的像记作$im\varphi=\{x\in G'\mid x=\varphi(a),a\in G\}$

**Def 2-5-4. 核：**同态$\varphi:G\rarr G'$的核记作$ker\varphi=\{a\in G\mid\varphi(a)=1\}$

**Lemma 2-5-2. **同态$\varphi:G\rarr G'$的像是$G'$的一个子群，核是$G$的一个子群

**Def 2-5-5. 交错群：**符号同态$S_n\rarr\{\pm1\}$的核称为交错群，记作$A_n$，由所有偶置换组成

**Def 2-5-6. 左陪集：**若$H$是$G$的子群，$a\in G$，则$aH=\{g\in H\mid g=ah,h\in H\}$，这个集合称为$H$在$G$中的左陪集

**Lemma 2-5-3. **令$\varphi:G\rarr G'$是一个群同态，$a,b\in G$，$K=ker\varphi$，则以下命题等价：

1. $\varphi (a)= \varphi(b)$
2. $a^{-1}b \in K$
3. $b \in aK$
4. $aK=bK$

**Ch 2-5-1.**同态$\varphi:G\rarr G'$为单射$\iff$$ker\varphi=\{1\}$

**Def 2-5-7. 共轭：**若$a,g\in G$，则$gag^{-1}$称为由$g$引出的$a$的共轭

**Def 2-5-8. 正规子群：**群$G$的子群$N$为正规子群，若$\forall a \in N,\forall g\in G,gag^{-1}\in N$

**Lemma 2-5-4. **若$\varphi:G\rarr G'$，则$ker\varphi$为正规子群

**Def 2-5-9. 群的中心：**群的中心$Z=\{z\in G\mid zx=xz,\forall x\in G\}$

### 6. 同构

**Def 2-6-1. 群同构：**双射群同态

**Ch 2-6-1. **若$\varphi:G\rarr G'$是同构，则其逆映射$\varphi^{-1}:G'\rarr G$也是同构

**Def 2-6-2. 群的同构关系：**若存在同构$\varphi:G\rarr G'$，则称$G$与$G'$同构，记作$G\approx G'$

**Def 2-6-3. 同构类：**与给定的群$G$同构的群形成群$G$的同构类

**Def 2-6-4. 自同构：**群$G$到其自身的同构

**Def 2-6-5. 共轭的元素：**若$\exists g \in G, x'=gxg^{-1}$，则称$x$与$x'$共轭

**Def 2-6-6. 交换子：**一个与元素对$a,b\in G$有关的元素$aba^{-1}b^{-1}$

**Lemma 2-6-1. **$a \in G$的共轭和$a$在群$G$中的阶相同

**Ch 2-6-2. **$ab=ba \iff aba^{-1}=b \iff aba^{-1}b^{-1}=1$

### 7. 等价关系、划分

**Def 2-7-1. 划分：**集合$S$的一个划分$\Pi$是将$S$的幂集的子集$\{E_i\}$，满足：$\bigcup\limits_{i=1}^nE_i=S$，$\forall E_i,E_j \in \Pi,E_i\cap E_j=\emptyset$

**Def 2-7-2. 等价关系：**集合$S$上的一个等价关系是一个元素对$a,b$之间的关系，记作$a\sim b$，满足以下条件：

1. 传递性：$a\sim b, b\sim c\implies a\sim c$
2. 对称的：$a\sim b\implies b\sim a$
3. 自反的：$\forall a \in S, a\sim a$

**Ch 2-7-1. **给定集合$S$上的等价关系，$S$的等价类构成$S$的划分

**Th 2-7-1. **集合$S$上的一个等价关系确定$S$上的一个划分，反之亦然

**Def 2-7-3. 堆：**集合$\bar S$表示给定划分下$S$的等价类的集合，当$S$的子集$U$作为$\bar S$中的元素考虑时，记作$[U]$

**Lemma 2-7-1. **对于任何等价关系，存在满射$\pi: S\rarr \bar S$，其中$\pi(a)=[C_a]=\bar a$

**Def 2-7-4. 映射定义的等价关系：**任一映射$f:S\rarr T$在其定义域$S$上定义了一个等价关系，也即规则：若$f(a)=f(b)$则$a\sim b$给出的等价关系

**Def 2-7-5. 纤维：**$t$关于映射$f$的原像集合称为映射$f$的纤维

**Lemma 2-7-2. **令$K$是同态$\varphi: G\rarr G'$的核，则$\varphi$的关于$G$中元素$a$的纤维是陪集$aK$，这些陪集构成了群$G$的划分，且每个划分对应着$im\varphi$的元素

### 8. 陪集

**Def 2-8-1. 同余关系：**$a,b \in G$，$H$为$G$的子集，$a$与$b$同余$\iff \exist h\in H,b=ah$，记作$a\equiv b$

**Lemma 2-8-1. **群$G$的子群$H$的左陪集是群$G$的划分

**Lemma 2-8-2. **若$H$是$G$的子群，$a, b \in G$，则下列结论等价：

1. $b = aH$对于某个$h \in H$成立，或$a^{-1}b \in H$成立
2. $b \in aH$
3. $aH = bH$

**Def 2-8-2. 指标：**一个子群$H$的互不相同的左陪集的个数称作其在群$G$中的指标，记作$[G:H]$

**Lemma 2-8-1. **群$G$的子群$H$的所有左陪集$aH$有相同的阶

> **Pf. **证明$H \rarr aH$的一个映射为双射

**Lemma 2-8-2. 计数公式：**$|G|=|H|[G:H]$

**Th. 2-8-3. Lagrange定理：**若$G$为有限群，$H$为$G$的子群，则$|H|\mid |G|$

**Ch. 2-8-2. **有限群的元素阶数整除群的阶数

**Ch. 2-8-3. **若群$G$的阶为$p$且$p$为素数，$\forall a \in G \and a \not= 1_G$，$G= \lang a \rang$

**Ch. 2-8-4. **若$\varphi:G\rarr G'$是有限群的一个同态，则：

1. $|G|=|ker\varphi|\cdot|im\varphi|$
2. $|ker\varphi|\mid |G|$
3. $|im\varphi|\mid|G|,|im\varphi|\mid |G'|$

**Lemma 2-8-3. 指标的乘法性质：**令$K\sub H \sub G$是群$G$的子群，则$[G:K]=[G:H][H:K]$

> **Pf. **假设$[G:H]$和$[H:K]$都是有限的，令$[G:H]=m,[H:K]=n$，则
>
> $\{g_1H,\cdots,g_mH\}$是$G$的一个划分，$\{h_1K,\cdots,h_mK\}$是$H$的一个划分
>
> 因此，$\{g_ih_1K,\cdots,g_ih_mH\}$是$g_iH$的一个划分
>
> 综上，可以构造$mn$个陪集$g_ih_iK$组成的$G$的一个划分

**Def 2-8-3. 右陪集：**群$G$的子群$H$的右陪集是集合$Ha=\{ha\mid h\in H\}$

**Def 2-8-4. 右同余：**$a\equiv b \iff \exist h \in H,b=ha$

**Lemma 2-8-4. **若群$H$为群$G$的子群，下列命题等价：

1. $H$是正规子群
2. $\forall g \in G, gHg^{-1}=H$
3. $\forall g \in G, gH=Hg$
4. $H$在$G$中的每个左陪集都是右陪集

**Lemma 2-8-5. **若$H$是群$G$的子群，且$g \in G$，则$gHg^{-1}$也是一个子群

**Lemma 2-8-6. **若群$G$只有一个$r$阶子群$H$，则$H$是正规的

### 9. 模算术

