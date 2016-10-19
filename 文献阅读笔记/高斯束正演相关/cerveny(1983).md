Červený, V. (1983). Synthetic body wave seismograms for laterally varying layered structures by the Gaussian beam method. Geophysical Journal International, 73(2), 389-426.

+ Three methods: the spectral method, the convolutory method and the wave-packet method.
+ (a system ogf Gaussian beam) The wavefield concentrated close to rays is evaluated by the parabolic equation equation method. Solutions of the parabolic wave equation (Schrodinger equation) decrease exponentially with the increasing square of distance from the ray. Thus, the the amplitude profile perpendicular to the ray is bell-shaped. This is the reason why these solutions are called Gaussian beams.
+ The Gaussian packets have approximately a bell-sharped envelope both in time and space.
+ Let us now consider a point _S_, situated close to the ray $\Omega$, specified by the ray-centred coordinates $(s,q_1,q_2)$, i.e. $S\equiv[s,q_1,q_2].$ The scalar Gaussian beam, connected with the central ray $\Omega$, then gives the following contribution at point _S_,
 $$ u(S,\omega)=A(s)exp\{i\omega\theta(s,q_1,q_2)-\omega G(S,q_1,q_2)\}.$$
Here $u(S,\omega)$ may represent various physical quantities in various wave propagation problems.The quantity $A(s)$ is a complex_valued amplitude factor which does not depend on $\omega$ and on the coordinates$q_1$, $q_2$. For Gaussian beams with a finite width, $A(s)$ remains finite along the whole ray $\Omega$; it has no singularity at the caustic. ... We shall call this function _the complexed_valued spreading_. It also contains the product of reflection/tyransmission coefficients. The phase factor $\theta(s,q_1,q_2)$ again does not depend on the frequency $\omega$, but it depends on all the three ray-centred coordinates of the point _S_, namely $s,q_1,q_2$.It is given by the relation $$\theta(s,q_1,q_2)=\tau(s)+\frac{1}{2v(s)}q^TK(s)q,$$
where
$$\tau(s)=\tau(s_0)+\int_{s_0}^s v^-1(\zeta)d\zeta, q^T=(q_1,q_2)$$
The integral is taken along $\Omega$ and $\zeta$ denotes the arc-length along $\Omega$. $K(s)$ is a $2\times2$ symmetrical real-valued matrix. It can be interpreted as the _curvature matrix of the phase front of the Gaussian beam_.
The expression $G(s,q_1,q_2)$ controls the decay of amplitudes of the Gaussian beam in the direction perpendicular to the ray $\Omega$, and can be expressed as $$G(s,q_1,q_2)=\frac{1}{2}q^TB(s)q$$
where $B(s)$ is a $2\times2$ positive definite real-valued matrix.
$$M(S)=\frac{1}{v(s)} K(s)+iB(s)$$
The quantity $M(s)$ may then be called the complex-valued _matrix of second derivatives of the travel-time field_ and $v(s) M(s)$ the complex-valued _curvature matrix_. Using $M(s)$, $$u(s,\omega)=A(s)exp\{i\omega [\tau(s)+\frac{1}{2}q^TM(s)q]\}$$
Matrix $M(s)$ is a complex-valued solution of the matrix Riccati equation,
$$\frac{dM}{ds}+vM^2+v^{-2}V=0$$
where $V(s)$ is a real_valued $2\times2$ matrix with elements $V_{ij}$ given by the expression
$$V_{ij}=[\partial^2V(s,q_1,q_2)/\partial q_i \partial q_j]_{q_1=q_2=0}.$$
The non-linear Riccati equation can be rewritten into a system of two matrix linear ordinary differential equations of the first order introducing new $2\times 2$ complex-valued matrices Q and P by the relations $M=v^{-1}dQ/dsQ^{-1}=PQ^{-1}$. The system reads
$$\frac{dQ}{ds}=vP,   \frac{dP}{ds}=-v^{-2}VQ.$$
The systems (last two equations) are called the _dynamic ray tracing systems_, and the matric $B$ and the quantity $G$ identically vanish.
+ assume that the corresponding system of rays is two-parametric and that it uniquely determines the system of wavefornts
We denote the two ray parameters by $\phi, \delta$. They may have a different meaning in different wave-propagation problems. They may correspond to some angles or direction cosines or slowness vector components in some problems, and may have the dimension of length in other problems.For example, in the case of a point source $\phi$ and $\delta$ may be taken as the take-off angles at the point source.They specify the initial direction of the ray at the source. In the case of a line source,$\phi$ may be the polar angle in the plane perpendicular to the line source and $\delta$ the length along the source, measured from some reference point at the line source. The ray parameters can also be specified along a selected wavefront of the wave; they may be regarded as curvilinear coordinates on the wavefront.
Let us assume that the medium in the vicinity of the source is locally homogeneous and again denote the observation point by $S$. We can then express the wavefield $U(S,\omega)$ as
$$U(S,\omega)=(-i\omega)^{k/2} \int_{\phi_0}^{\phi_N} \int_{\delta_0}^{\delta_M}\Phi(\phi,\delta)u(S,\omega,\phi,\delta)d\phi d\delta$$
$\Phi(\phi,\omega)$ is some complex-valued function not specified here, which depends on the type of source.The limits in both integrals, $\phi_0$, $\phi_N$, and $\delta_0$, $\delta_M$, may be different for different sources. ... For a 3D case, with a double integral, the quantity $k$ was found to equal 2. The equation can also be applied to a 2-Dcase.Then it contains only one integral over $\phi$, and $k$ equals 1.
The expression $u(S,\omega,\phi,\delta)$ for Gaussian beams can be used only in the regularity region along the ray $\Omega$ specified by the ray parameters $\phi,\delta$. Therefore, the function $u(S,\omega,\phi,\delta)$ in the integral should be multiplied by some windowing function which vanishes outside the regularity region.
When the integrand is sufficiently smooth for given $S$ and $\omega$, the integral may be evaluated by numerical quadratures. This gives
$$U(S,\omega)=(-i\omega)^{k/2} \sum_{i=0}^{N} \sum_{j=0}^{M}\Phi(\phi_i,\delta_j)u(S,\omega,\phi_i,\delta_j)\Delta\phi_i \Delta\delta_j$$
where the quantities $\Delta \phi_i$ and $\Delta \delta_j$ are determined from a given system of $\phi_i$ and $\delta_j$ $(i=0,1,2,...,N;j=1,1,...,M)$ in agreement with specific quadrature procedure.
+ When the receiver point is situated close to the Earth's surface, all the necessary parameters of Gaussian beams can be determined from the termination points of the rays along the Earth's surface. In this way, only the termination points of the rays at the Earth's surface (not the whole rays) together with the auxiliary quantities determined at these points can be stored in the computer.
+ We denote the source_time function by $f(t)$. We denote the spectrum of $f(t)$ by $F(\omega)$,
$$f(t)=\frac{1}{\pi} Re\int_0^{\infty}F(\omega)exp(-i\omega t)d\omega$$
We assume that $f(t)$ is a high-frequency functions. This means that the Fourier spectrum $F(\omega)$ of $f(t)$ effectively vanishes for small frequencies.
Using the Fourier transform, we obtain
$$U(S,t)=\frac{1}{\pi}Re \int_0^{\infty} (-i\omega)^{k/2} F(\omega)exp(-i\omega t)\int_{\phi_0}^{\phi_N} \int_{\delta_0}^{\delta_M}\Phi(\phi,\delta)\times u(S,\omega,\phi,\delta)d\phi d\delta d\omega.$$
The above expression can be ewwritten in the following form
$$U(S,t)=\frac{1}{\pi}Re \int_0^{\infty} (-i\omega)^{k/2} F(\omega)\int_{\phi_0}^{\phi_N} \int_{\delta_0}^{\delta_M}\Phi(\phi,\delta)A exp(-\omega G)\times exp[-i\omega(t-\theta)]d\phi d\delta d\omega,$$
where $A=A(s,\phi,\delta)$, $G=G(s,q_1,q_2,\phi,\delta)$, $\theta=\theta(s,q_1,q_2,\phi,\delta)$.
+ Rewrite in the following form
$$U(s,t)=\int_{\phi_0}^{\phi_N} \int_{\delta_0}^{\delta_M}g(S,t,\phi,\delta)d\phi d\delta,$$
where
$$g(S,t,\phi,\delta)=\frac{1}{\pi} Re \{\Phi \int_0^{\infty}(-i\omega)^{k/2}F(\omega)A\ exp(-\omega G)exp[-i\omega(t-\theta)d\omega]\}$$
We can call function $g(S,t,\phi,\delta)$ the wave packet.
+ Write approximate expressions for the wave packet. Let us consider the wavelet $f(t)$ given by the formula
$$f(t)=exp[-(2\pi f_M t/\gamma)^2]cos(2\pi f_M t +v)$$
with three free parameters, $f_M$, $\gamma$, v. (This) wavelet corresponds to a harmonic carrier with a Gaussian (bell-shaped) envelope. The quantity $\gamma$ controls the width of the Gaussian envelope, with respect to the prevailing frequency $f_M$. We assume that the prevailing frequency $f_M$ is high. The envelope is narrow for small $\gamma$ and broad for large $\gamma$.
Gaussian wave packet $g(S,t,\phi,\delta)$ is as follows,
$$g(S,t,\phi,\delta)=(2 \pi f_M)^{k/2}|\Phi A|\ exp \{-[2\pi f_M(t-\theta)/\gamma]^2+4\pi^2 f_M^2G^2/\gamma^2-2\pi f_M G\}
\times cos\{2\pi f^*(t-\theta)+v-arg(\Phi A)+k\pi/4\}$$
The Gaussian packets have an approximately Gaussian envelope both in space and time. The envelope is strictly Gaussian in the time domin and does not change as the wave progresses. In the direction perpendicular to the ray, the envelope is not strictly Gaussian; we have obtained two terms depending on $G$ and $G^2$ in the expression for the envelope.
+ The Gaussian packet approach does not require two-point ray tracing; it is sufficient to compute the rays as an initial-value problem and cover the region where the receivers are situated by these rays.
The Gaussian packet approach is not so sensitive to details of the velocity distribution in the model as the ray method, so that simpler approximation can be used to determine the velocity distribution from the network of velocity points.
