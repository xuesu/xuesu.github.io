#DSP
##1.Introduction
###History
1. Pythagoras
	
	Most Reality can be described in terms of numbers and measurement

2. Parmenides

	plant the seed of fndemental dichotomy, the fundemental difference between the reality and the ideal reality

3. Plato
	
	metaphysics

4. Zeno's Paradox
5. Galileo's Calculus and Descartes' Coordinate
6. Fourier Analysis
7. Nyquist and Shanon: The Sampling Theorem
###discretization:time or amplitude
the amplitude discretization are good for storage,processing and transmission
###Attenuation and Noise
because of Noise, the digital signal is better
##2.1 Discrete time signals
###discrete time signals

- a sequence of complex numbers
	- notation: x[n]
		- n: integer, dimention-less "time"
	- two-side sequences: x: z->c
	- analysis: periodic measurement
	- synthesis: stream of generated samples

###examples
####Delta signal
![](http://i.imgur.com/1aAYGN8.png)
####The unit step
![](http://i.imgur.com/mQND81O.png)
####The exponential decay
![](http://i.imgur.com/kaDbH3V.png)
x[n]\(n < 0) is 0 because it will unbounded 
####Sinusoid
![](http://i.imgur.com/WOucGGy.png)
###Four Signal Classes
- Finite-Length Signal
- Infinite-Length Signal
- Periodic
	- ![](http://i.imgur.com/1DWedfI.png)
- Finite-Support
	- ![](http://i.imgur.com/adNZU0Q.png)
###Elementary operators
- scaling
	- <img src="http://www.forkosh.com/mathtex.cgi? $y[n]=\alpha x[n]$">
- sum
	- y[n] = x[n] + z[n]
- product
	- y[n] = x[n] * z[n]
- shift by k(decay)
	- y[n] = x[n - k]
	- shift of a finite-length:finite support
		- ![](http://i.imgur.com/oh680Kz.png)
	- shift of a finite-length:periodic extension
		- ![](http://i.imgur.com/EdFjCCv.png)
- Energy
	- <img src="http://www.forkosh.com/mathtex.cgi? $E_x=\sum_{n=-\infty}^{+\infty}{\left|x[n] \right|}^2$"/>
- Power
	- <img src="http://www.forkosh.com/mathtex.cgi? $P_x=\lim_{N \to \infty} \frac{1}{2N+1} \sum_{n=-N}^N{\left|{x[n]} \right|}^2"/>
	- The window's size is 2N+1
- Energy&Power:Periodic Signal
		- <img src="http://www.forkosh.com/mathtex.cgi? $E_{\tilde{x}}= \infty$" />
	- Energy  
		- <img src="http://www.forkosh.com/mathtex.cgi? $E_{\tilde{x}}= \infty$" />
	- Power
		- <img src="http://www.forkosh.com/mathtex.cgi? $P_{\tilde{x}}= \frac{1}{N} \sum_{n=0}^{N-1}{\left| {\tilde{x}[n]} \right|}^2$" />

##2.2 The Complex Exponential
###Complex Exponential
- The oscillatory heartbeat is measured by:
	- a frequency <img src="http://www.forkosh.com/mathtex.cgi? $\omega$" />(unit:radians)
	- an initial phase  <img src="http://www.forkosh.com/mathtex.cgi? $\phi$" />(unit:radians)
	- an amplitude A
	- a trigonometric function <img src="http://www.forkosh.com/mathtex.cgi? $x[n]=Acos(\omega n+\phi)$" />
- The Euler's formulas
	-  <img src="http://www.forkosh.com/mathtex.cgi? $x[n]=Acos(\omega n+\phi)+Ajsin(\omega n+\phi)=e^{j(\omega n+\phi)}$" />
-  The advantages of using complex exponentials rather than trigonometric
	-  sine & cosine "live" together
	-  phase shift is simple multiplication
		-  ![](http://i.imgur.com/BI3b3Hj.png)
###Periodic
- ![](http://i.imgur.com/CX7E15b.png)
- Attention: Not all sinusiod is periodic
- Periodic when:<img src="http://www.forkosh.com/mathtex.cgi? $x[n]=e^{j(\omega n+\phi)},\omega=\frac{M}{N}2\pi (M,N\in N)$" />
- so <img src="http://www.forkosh.com/mathtex.cgi? $x[n]=e^{j(\omega n+\phi)}=e^{j(\omega n+\phi +2\pi)}$" />
###<b>Wagonwheel effect</b>
- when the <img src="http://www.forkosh.com/mathtex.cgi? $\omega$" /> is larger and larger, when it is near <img src="http://www.forkosh.com/mathtex.cgi? 2$\pi$" /> we can see the wagonwheel seems stop
###Discrete time frequency vs. Physical time frequecy
- Discrete
	- n: no physical dimension
	- periodicty: samples
- Physical
	- measured in Hz
- ![](http://i.imgur.com/Pz3Cvmn.png)
	- where system clock take part in interpolation
	- The real frequency is <img src="http://www.forkosh.com/mathtex.cgi? $f=MT_s$" />