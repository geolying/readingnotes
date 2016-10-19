Bleistein, N. (2009). Mathematics of modeling, migration and inversion with
Gaussian beams, Lecture Notes,[www.cwp.mines.edu/~norm/](http://www.cwp.mines.edu/~norm/)
+ Gaussian beams are
    Ray-theory with complex traveltimes;
    Best described in ray-centred coordinates；
    Computed in Cartesian coordinates.
+ Ray-theory: extension of WKBJ method
        ODEs to PDEs
        Amplitude$\to$first term of series
+ Modeling with Gaussian beams
  Smoother than classic ray theory
  Best near caustics
  Eage? Still problems
+ Ray-centered coordinates, Eikonal equation
$$(\frac{\partial \Phi}{\partial s})^2+h^2(\frac{\partial \Phi}{\partial n})^2=\frac{h^2}{v^2}$$
Power series in $n$ for $\Phi$:
$$\Phi=\Phi_0(s)+n\Phi_1+\frac{n^2}{2}\Phi_2(s)$$
Leading order equation in $n$:
$$(\frac{d\Phi_0}{ds})^2+\Phi_1^2=\frac{1}{v_0^2}$$
$$\frac{d\Phi_0}{ds}=\frac{1}{v_0}\ and\ \Phi_1=0$$
Second order in $n$:
$$\frac{d\Phi_2}{ds}+v_0\Phi_2^2+\frac{v_{0,nn}}{v_0^2}=0$$
$$\Phi_2=\frac{1}{v_0Q}\frac{dQ}{ds}$$
(Leads to 2nd order ODE for Q or first order system)
$$\frac{dQ}{ds}=v_0P,\ \frac{dP}{ds}=-\frac{v_{0,nn}}{v_0^2}Q$$
$$\Phi_2=\frac{P}{Q}$$
Solution for $\Phi$:
$$\Phi(n,s)=\tau_0+\int_{s_0}^s\frac{ds'}{v_0(s')}+\frac{n^2}{2}\frac{P}{Q}$$
Amplitude:
$$\frac{d}{s}(\frac{A_0^2}{v_0})+\frac{A_0^2}{v_0}\frac{Q_{,s}}{Q}=0 \Leftrightarrow \frac{d}{ds}(\frac{QA_0^2}{v_0})=0$$
$$A_0(n,s)=constant\sqrt{\frac{v_0}{Q}}$$
$$u(n,s)=\sqrt{\frac{v_0(s)}{Q(s)}}exp\{i\omega\Phi(n,s)\}$$
<font color=red>(Q～距离，P～慢度)</font>
