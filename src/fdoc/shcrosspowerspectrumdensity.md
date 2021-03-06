# SHCrossPowerSpectrumDensity

Compute the cross-power spectral density of two real functions.

# Usage

call SHCrossPowerSpectrumDensity (`cilm1`, `cilm2`, `lmax`, `cspectrum`)

# Parameters

`cilm1` : input, real\*8, dimension (2, `lmaxin1`+1, `lmaxin1`+1)
:   The first function expressed in real spherical harmonics.

`cilm2` : input, real\*8, dimension (2, `lmaxin2`+1, `lmaxin2`+1)
:   The second function expressed in real spherical harmonics.
	
`lmax` : input, integer
:   The maximum spherical harmonic degree to calculate the cross-power spectral density. This must be less than or equal to the minimum of `lmaxin1` and `lmaxin2`.

`cspectrum` : output, real\*8, dimension (`lmax`+1)
:   The cross-power spectral density of the two functions.

# Description

`SHCrossPowerSpectrumDensity` will calculate the cross-power spectral density of two functions expressed in real spherical harmonics. For a given spherical harmonic degree `l`, this is explicitly calculated as:

`cspectrum(l) = Sum_{i=1}^2 Sum_{m=0}^l cilm1(i, l+1, m+1) * cilm2(i, l+1, m+1) / (2l + 1)`.

# See also

[shpowerl](shpowerl.html), [shpowerdensityl](shpowerdensityl.html), [shcrosspower](shcrosspower.html), [shcrosspowerdensityl](shcrosspowerdensityl.html), [shpowerspectrum](shpowerspectrum.html), [shpowerspectrumdensity](shpowerspectrumdensity.html), [shcrosspowerspectrum](shcrosspowerspectrum.html), [shadmitcorr](shadmitcorr.html)
