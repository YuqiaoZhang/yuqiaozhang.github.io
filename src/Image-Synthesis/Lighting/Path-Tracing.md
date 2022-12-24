# Path Tracing

## Rendering Equation  

The **Rendering Equation** is also called the **LTE** (**Light Transport Equation**) by "14.4 The Light Transport Equation" of [PBR Book](https://www.pbr-book.org/3ed-2018/Light_Transport_I_Surface_Reflection/The_Light_Transport_Equation). And we have the **Rendering Equation** $\displaystyle \operatorname{L_o}(\overrightarrow{p}, \overrightarrow{\omega_V}) = \operatorname{L_e}(\overrightarrow{p}, \overrightarrow{\omega_V}) + \int_\Omega \operatorname{f}(\overrightarrow{p}, \overrightarrow{\omega_L}, \overrightarrow{\omega_V}) \operatorname{L_i}(\overrightarrow{p}, \overrightarrow{\omega_L}) (\cos \theta_L)^+ \, d \overrightarrow{\omega_L}$.   

## Fredholm Integral Equation  

By "Figure 11.1" of [Real-Time Rendering Fourth Edition](http://www.realtimerendering.com/) and "Figure 14.14" of [PBR Book](https://pbr-book.org/3ed-2018/Light_Transport_I_Surface_Reflection/The_Light_Transport_Equation), by assuming no participating media, we have the relationship $\displaystyle \operatorname{L_i}(\overrightarrow{p}, \overrightarrow{\omega_L}) = \operatorname{L_o}(\operatorname{r}(\overrightarrow{p}, \overrightarrow{\omega_L}), -\overrightarrow{\omega_L})$ where $\displaystyle \operatorname{r}(\overrightarrow{p}, \overrightarrow{\omega})$ is the ray-casting function. This means that the incident radiance $\displaystyle \operatorname{L_i}(\overrightarrow{p}, \overrightarrow{\omega_L})$ at one point p is exactly the exitant radiance $\displaystyle \operatorname{L_o}(\operatorname{r}(\overrightarrow{p}, \overrightarrow{\omega_L}), -\overrightarrow{\omega_L})$ at another point $\displaystyle \operatorname{r}(\overrightarrow{p}, \overrightarrow{\omega_L})$.  

Hence, both the incident radiance $\displaystyle \operatorname{L_i}(\overrightarrow{p}, \overrightarrow{\omega})$ and the exitant radiance $\displaystyle \operatorname{L_o}(\overrightarrow{p}, \overrightarrow{\omega})$ can be represented by the same function $\displaystyle \operatorname{L}(\overrightarrow{p}, \overrightarrow{\omega})$. And thus, we have $\displaystyle \operatorname{L}(\overrightarrow{p}, \overrightarrow{\omega_V}) = \operatorname{L_e}(\overrightarrow{p}, \overrightarrow{\omega_V}) + \int_\Omega \operatorname{f}(\overrightarrow{p}, \overrightarrow{\omega_L}, \overrightarrow{\omega_V}) \operatorname{L}(\operatorname{r}(\overrightarrow{p}, \overrightarrow{\omega_L}), -\overrightarrow{\omega_L}) (\cos \theta_L)^+ \, d \overrightarrow{\omega_L}$ which is an integral equation where the unknown function is $\displaystyle \operatorname{L}(\overrightarrow{p}, \overrightarrow{\omega})$.  

According to this integral equation, by [OSL (Open Shading Language)](https://github.com/AcademySoftwareFoundation/OpenShadingLanguage), the surface and the light are actually the same thing, since the light is merely the surface which is emissive.  

By "Light transport and the rendering equation" of [CS 348B - Computer Graphics: Image Synthesis Techniques](http://www-graphics.stanford.edu/courses/cs348b-96/) and "Global Illumination and Rendering Equation" of [CS 294-13 Advanced Computer Graphics](https://inst.eecs.berkeley.edu/~cs294-13/fa09/), this integral equation is actually the [Fredholm Integral Equation](https://en.wikipedia.org/wiki/Fredholm_integral_equation) of which the solution is the [Liouville–Neumann Series](https://en.wikipedia.org/wiki/Liouville%E2%80%93Neumann_series). And thus, the solution of this integral equation can be written as the recursive form $\text{L} = \text{E} + \text{K}\text{E} + {\text{K}}^2\text{E} + {\text{K}}^3\text{E} + \ldots$.  

## The Area Form 

## The Path Form  

// ray-casting function eliminate  
// area form  
// visibility function  

// throughput 14.18  

By "Equation \(14.19\)" of [PBR Book](https://pbr-book.org/3ed-2018/Light_Transport_I_Surface_Reflection/Path_Tracing#IncrementalPathConstruction), we have the relationship between the area PDF and the solid angle PDF $\displaystyle \operatorname{p_A}(p_i) = \frac{\cos\theta_i}{{\|p_{i+1} - p_i\|}^2} \operatorname{p_{\omega}}(\widehat{p_{i+1} \rightarrow p_i})$. Here is the proof of this relationship. By "Equation (5.6)" of [PBR Book](https://pbr-book.org/3ed-2018/Color_and_Radiometry/Working_with_Radiometric_Integrals#IntegralsoverArea), we have the relationship between the differential area and the differential solid angle $\displaystyle d\omega = \frac{\cos\theta}{r^2}dA \Rightarrow dA = \frac{r^2}{\cos\theta}d\omega$. Since $\displaystyle \operatorname{p_A}$ is the area PDF, we have $\displaystyle \int_A \operatorname{p_A}(p_i) \, d\operatorname{A}(p_i) = 1 \Rightarrow \displaystyle \int_A \operatorname{p_A}(p_i) \, d\operatorname{A}(p_i) = \int_A \operatorname{p_A}(p_i) \, (\frac{{\|p_{i+1} - p_i\|}^2}{\cos\theta_i} d\operatorname{\omega}(\widehat{p_{i+1} \rightarrow p_i})) = \int_{\Omega} (\operatorname{p_A}(p_i) \frac{{\|p_{i+1} - p_i\|}^2}{\cos\theta_i}) \, d\operatorname{\omega}(\widehat{p_{i+1} \rightarrow p_i}) = 1$. Since $\displaystyle \operatorname{p_{\omega}}$ is the solid angle PDF, we have $\displaystyle \int_{\Omega} \operatorname{p_{\omega}}(\widehat{p_{i+1} \rightarrow p_i}) \, d\operatorname{\omega}(\widehat{p_{i+1} \rightarrow p_i}) = 1 \Rightarrow \operatorname{p_{\omega}}(\widehat{p_{i+1} \rightarrow p_i}) = \operatorname{p_A}(p_i) \frac{{\|p_{i+1} - p_i\|}^2}{\cos\theta_i} \Rightarrow \operatorname{p_A}(p_i) = \frac{\cos\theta_i}{{\|p_{i+1} - p_i\|}^2} \operatorname{p_{\omega}}(\widehat{p_{i+1} \rightarrow p_i})$.  

// appeal pA = ... pw to 14.17, we have 14.19 (last vertex remains the differential area, change all other vertices to differential solid angle)  

## Incremental Path Construction  

// when evaluate p(i+1), the result of previous path p(i) is **reused**  
// for example, the **beta** is reused // **beta** in 14.5.4 Implementation  
// introduce correlation but the result is not bad  