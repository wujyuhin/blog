#gdina #cdm #R
[模型估计和模型诊断 • GDINA (wenchao-ma.github.io)](https://wenchao-ma.github.io/GDINA/articles/OnlineExercises/CDMAnalysis_example.html)


R 语言中的拟合度指标计算
anova 需要带入一个 dina 模型对象
anova. Din 模型中使用了 IRT. IC
IRT. IC 模型中又调用了 logLik

```R
Q <- matrix(c(1,0,0,
              0,1,0,
              0,0,1,
              1,0,1,
              0,1,1,
              1,1,0,
              1,0,1,
              1,1,0,
              1,1,1,
              1,0,1),byrow = T,ncol = 3)

Q1<- matrix(c(1,1,1,
              0,1,1,
              0,1,0,
              1,0,1,
              0,1,0,
              1,1,1,
              1,0,1,
              1,1,0,
              1,0,1,
              1,1,1),byrow = T,ncol = 3)
est.Q <- GDINA(dat,Q,model="DINA",verbose = 0)
est.Q1 <- GDINA(dat,Q1,model="DINA",verbose = 0)
anova(est.Q, est.Q2)

# 通过源码查询发现
logLik 中的输入是 list(est.Q, est.Q1)[[1]]
即logLik(est.Q)!!!
```

## LogLik 源码
![[Pasted image 20240525163257.png]]
## extract 源码
到头来发现妈的，原来放进来的 object 中已经算好了 $-2Log$ 了，这里是反算回对数似然
![[Pasted image 20240525164301.png]]

所以还是得看 GDINA 模型中计算 Deviance 是怎么算的
## GDINA 源码
![[Pasted image 20240525165543.png]]
### 查看 SG.Est 源码
![[Pasted image 20240525165645.png]]
### 里面有个 ObsLogLik 函数是计算似然函数的
```R
需要item.parm[[i]]
dat
logprior
rep(1,N)
parloc
freq
```
T 他妈的到 ObsLogLik 里面出来个 call 函数，找不到了