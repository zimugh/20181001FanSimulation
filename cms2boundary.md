
<h1>Table of Contents<span class="tocSkip"></span></h1>
<div class="toc"><ul class="toc-item"><li><span><a href="#CMS-boundary-condition-and-grid-structure" data-toc-modified-id="CMS-boundary-condition-and-grid-structure-1"><span class="toc-item-num">1&nbsp;&nbsp;</span>CMS boundary condition and grid structure</a></span><ul class="toc-item"><li><span><a href="#A-reference" data-toc-modified-id="A-reference-1.1"><span class="toc-item-num">1.1&nbsp;&nbsp;</span>A reference</a></span></li></ul></li></ul></div>

## CMS boundary condition and grid structure
In CMS Version 2.0, the object of interest (e.g., an active region or filament) is modeled with
high spatial resolution (the HIRES region), and the more distant regions are modeled with a lower
resolution, global potential field (GLOBAL region).The HIRES region is a NLFF field and the GLOBAL region is a potential field. The model we export is NLFF field in the HIRES region which is the domain used as initial condition of the MHD simulation. 
- Both regions use the spherical coordinate system ($r$,$\theta$ ,$\phi$ )
  - where r is the radial distance from Sun center, 
  - $\theta$ is the polar angle relative to the solar rotation axis, We frequently use the latitude $\lambda$ ($\pi/2-\theta$) instead of the polar angle,
  - and $\phi$ is the azimuth angle which is measured relative to the central meridian as seen from Earth at the model time.
  - $\theta_{min}<\theta<\theta_{max}$ & $\lambda_{min}<\lambda<\lambda_{max}$ & $r_{\odot}<r<r_{max}$
    - $r=r_{\odot}$ where the magnetic field is observed photosphere field and $r=r_{max}$ where the magnetic field becomes radial,
    - At the side boundaries of the domain, the magnetic field lines pass from the HIRES region into the GLOBAL region. The normal component of the magnetic field needs to be continuous at these side boundaries, but there may be small discontinuities in the tangential components.
    
- In the HIRES region, the vector potential A(r), magnetic field B(r), and current density j(r)
are discretized on staggered grids.
  - $A_{\phi}$ and $j_{\phi}$ are defined at the centers of the x-edges of the cells (halfway between two corner points),$A_{\theta}$ and $j_{\theta}$ are defined on the y-edges and $A_{r}$ and $j_{r}$ are defined on the z-edges.
  - The magnetic field $B_{\phi}$ is defined at the centers of the x-face (between four corner points), and similar for B$B_{\theta}$ and $B_{r}$.

### A reference 
1. Yang Guo2019 http://adsabs.harvard.edu/abs/2019ApJ...870L..21G
   - Solar Magnetic Flux Rope Eruption Simulated by a Data-Driven Magnetohydrodynamic Model
     - MHD model:zero-$\beta$ approximation
     - Initial conditions:(Page 4)
       - B:NLFF field from extrapolation
       - $\rho$:solving the hydrostatic equation
       - The initial condition for the velocity is zero for all the three components
     - Boundary conditions:(Page 5)
       - Data-driven boundary condition
       - Data-constrained boundary condition
       
   - My Inspiration (picture 5)
      1. The 20 minutes shift between observation and simulation may be due to the 1-D distribution $\rho$.  It will take less time to lead to the eruption if ignore the 3-D distribution $\rho$, because $\rho$ in flux rope (filaments) is higher than ambient environment, which should prevent the eruption.
      2. The difference eruption velocity between observation and simulation may be also due to the 1-D distribution $\rho$ or the limitations of the zero-$\beta$ simulation.
      3. To obtain the 3-D distribution $\rho$ which is consistent with the NLFF field B, deep learning may be helpful.
      4. GAN neural network can serve as a method that translate B to $\rho$, P, v. We use the previous simulation results as the train data to build the mapping between B and other physical characteristics($\rho$, P, v). And then produce related $\rho$, P, v of a new B through the trained GAN neural network, set them as the initial conditions of a MHD simulaiton.
      
    
 


```python




```





