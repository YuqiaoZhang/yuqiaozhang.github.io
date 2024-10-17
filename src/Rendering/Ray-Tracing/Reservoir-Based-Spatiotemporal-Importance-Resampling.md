
# ReSTIR (Reservoir-Based Spatiotemporal Importance Resampling)  

## Reservoir Sampling  

### Basic Reservoir Sampling  

By "A.2 Reservoir Sampling" of [PBR Book V4](https://www.pbr-book.org/4ed/Sampling_Algorithms/Reservoir_Sampling#), we have the **basic reservoir sampling**.  
   
We sequentially process each **sample** from the **stream**. The total length of the **stream** can indeed be infinite which is too large to be stored in the memory.   

We assume that we have processed **n** **samples**. This means that the number of the **seen samples** is **n**. For the **basic reservoir sampling**, the **reservoir** can hold at most **1** **reservoir sample**, and the first **1** **seen** **sample** is always selected to initialize the **reservoir**. For each subsequent **seen** **candidate sample**, we have the probability $\displaystyle \frac{1}{n}$ of selecting it to replace the existing **sample** within the **reservoir**.  

We can prove by **mathematical Induction** that at any iteration, when we have processed n **samples**, each **sample** from the **stream** has the equal probability $\displaystyle \frac{1}{n}$ of being included in the final **reservoir**.  

> Base Case  
>>
>> At the iteration, when we have processed n = 1 **sample**, each **sample** has the equal probability $\displaystyle \frac{1}{1} = 1$ of being included in the final **reservoir**.  
>  
> Inductive Step  
>> 
>> We assume that at the iteration, when we have processed n = k **samples**, each **sample** from the **stream** has the equal probability $\displaystyle \frac{1}{k}$ of being included in the final **reservoir**.  
>>   
>> And we would like to prove that at the iteration, when we have processed n = k + 1 **samples**, each **sample** from the **stream** has the equal probability $\displaystyle \frac{1}{k + 1}$ of being included in the final **reservoir**.  
>>  
>> Evidently, the (k + 1)-th **seen sample** has the probability $\displaystyle \frac{1}{k + 1}$ of being selected to replace the existing **sample** within the **reservoir** and thus being included in the final **reservoir**.  
>>  
>> For the previous k **seen samples**, they have the probability $\displaystyle \frac{1}{k}$ of being included in the final **reservoir** at k-th iteration. At the same time, they have the probability $\displaystyle 1 - \frac{1}{k + 1} = \frac{k}{k + 1}$ of NOT being replaced by the (k + 1)-th **seen sample** at (k + 1)-th iteration. This means that they have the probability $\displaystyle \frac{1}{k} \times \frac{k}{k + 1} = \frac{1}{k + 1}$ of being included in the final **reservoir** at (k + 1)-th iteration.  

## References  

\[Wyman 2023\] [Chris Wyman, Markus Kettunen, Daqi Lin, Benedikt Bitterli, Cem Yuksel, Wojciech Jarosz, Pawel Kozlowski, Giovanni Francesco. "A Gentle Introduction to ReSTIR: Path Reuse in Real-time." SIGGRAPH 2023.](https://intro-to-restir.cwyman.org/)  