# SHExpandDH  

Expand an equally sampled or equally spaced grid into spherical harmonics using Driscoll and Healy's (1994) sampling theorem.

# Usage

call subroutine SHExpandDH (`griddh`, `n`, `cilm`, `lmax`, `norm`, `sampling`, `csphase`, `lmax_calc`)

# Parameters

`griddh` : input, real\*8, dimension (`n`, `n`) or (`n`, 2\*`n`)
:   A 2D equally sampled (default) or equally spaced grid that conforms to the sampling theorem of Driscoll and Healy (1994). The first latitudinal band corresponds to 90 N, the latitudinal band for 90 S is not included, and the latitudinal sampling interval is 180/`n` degrees. The first longitudinal band is 0 E, the longitude band for 360 E is not included, and the longitudinal sampling interval is 360/`n` for an equally and 180/`n` for an equally spaced grid, respectively.

`n` : input, integer
:   The number of samples in latitude of `griddh`. If `sampling` is 1 (default) then the number of samples in longitude is `n`. If `sampling` is 2 then the number of longitudinal samples is `2n`. `n` must be even.
	
`cilm` : output, real\*8, dimension (2, `n`/2, `n`/2) or (2, `lmax_calc`+1, `lmax_calc`+1) 
:   The real spherical harmonic coefficients of the function. These will be exact if the function is bandlimited to degree `lmax=n/2-1`. The coefficients `c1lm` and `c2lm` refer to the cosine (`clm`) and sine (`slm`) coefficients, respectively, with `clm=cilm(1,l+1,m+1)` and `slm=cilm(2,l+1,m+1)`.
	
`lmax` : output, integer
:   The maximum spherical harmonic bandwidth of the input grid, which is `n/2-1`. If the optional parameter `lmax_calc` is not specified, this corresponds to the maximum spherical harmonic degree of the output coefficients `cilm`.

`norm` : input, integer, optional, default = 1
:   1 (default) = 4-pi (geodesy) normalized harmonics; 2 = Schmidt semi-normalized harmonics; 3 = unnormalized harmonics; 4 = orthonormal harmonics.

`sampling` : input, integer, optional, default = 1
:   If 1 (default) the input grid is equally sampled (`n` by `n`). If 2, the grid is equally spaced (`n` by `2n`).

`csphase` : input, integer, optional, default = 1
:   1 (default) = do not apply the Condon-Shortley phase factor to the associated Legendre functions; -1 = append the Condon-Shortley phase factor of (-1)^m to the associated Legendre functions.

`lmax_calc` : input, integer, optional, default = `lmax`
:   The maximum spherical harmonic degree calculated in the spherical harmonic expansion.

# Description

`SHExpandDH` will expand an equally sampled (`n` by `n`) or equally spaced grid (`n` by `2n`) into spherical harmonics using the sampling theorem of Driscoll and Healy (1994). The number of latitudinal samples, `n`, must be even, and the transform is exact if the function is bandlimited to spherical harmonic degree `n/2-1`. The inverse transform is given by the routine `MakeGridDH`. If the optional parameter `lmax_calc` is specified, the spherical harmonic coefficients will only be calculated to this degree instead of `n/2-1`. The algorithm is based on performing FFTs in longitude and then integrating over latitude using an exact quadrature rule. 

The default is to use an input grid that is equally sampled (`n` by `n`), but this can be changed to use an equally spaced grid (`n` by `2n`) by the optional argument `sampling`.  When using an equally spaced grid, the Fourier components corresponding to degrees greater than `n/2-1` are simply discarded; this is done to prevent aliasing that would occur if an equally sampled grid was constructed from an equally spaced grid by discarding every other column of the input grid.

The employed spherical harmonic normalization and Condon-Shortley phase convention can be set by the optional arguments `norm` and `csphase`; if not set, the default is to use geodesy 4-pi normalized harmonics that exclude the Condon-Shortley phase of (-1)^m. The normalized legendre functions are calculated in this routine using the scaling algorithm of Holmes and Featherstone (2002), which are accurate to about degree 2800. The unnormalized functions are accurate only to about degree 15. 

# References

Driscoll, J.R. and D.M. Healy, Computing Fourier transforms and convolutions on the 2-sphere, Adv. Appl. Math., 15, 202-250, 1994.

Holmes, S. A., and W. E. Featherstone, A unified approach to the Clenshaw summation and the recursive computation of very high degree and order normalised associated Legendre functions, J. Geodesy, 76, 279-299, 2002.

# See also

[`makegriddh`](makegriddh.html), [`makegriddhc`](makegriddhc.html), [`shexpanddhc`](shexpanddhc.html), [`makegridglq`](makegridglq.html), [`shexpandglq`](shexpandglq.html), [`makegridglqc`](makegridglqc.html), [`shexpandglqc`](shexpandglqc.html), [`shexpandlsq`](shexpandlsq.html)