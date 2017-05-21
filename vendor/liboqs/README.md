liboqs (with OKCN-LWE and OKCN-LWR added)
======

**This is a fork from [liboqs](https://github.com/open-quantum-safe/liboqs)**.

Overview
--------

This fork provides implementations and benchmark comparisons between OKCN-LWE, OKCN-LWR and previous proposed key exchange schemes.
Most of the codes are modified or copied from `kex_lwe_frodo` in original liboqs project.

|Operation |  Time(us): mean  |  pop. stdev  |  CPU Cycles: mean  |  pop. stdev |
|----------|-----------------:|-------------:|---------------:|------------:|
|RLWE BCNS15																																|
|alice 0	 |	1031.648        | 6.987        | 2367223        | 15992       |
|bob			 |	1663.542        | 13.207       | 3817186        | 30319			  |
|alice 1   |  215.962         | 3.819        | 495438         |  8712       |
|RLWE NewHope |
|alice 0   |  85.618          | 2.148        | 196366         |  4831				|
|bob       |  128.008         | 3.791        | 293647         |  8650				|
|alice 1   |  26.316          | 1.291        | 60290          |  2787				|
|RLWE MSR LN16 |
|alice 0   |  79.441          | 2.496        | 182188         |  5636				|
|bob       |  130.848         | 2.419        | 300145         |  5460				|
|alice 1   |  23.231          | 1.081        |  53217         |  2303				|
|LWE Frodo recommended |
|alice 0   |  1370.805        | 7.387        | 3145480        |  16916      |
|bob       |  1921.255        | 12.146       | 4408558        |  27804			|
|alice 1   |  144.894         | 2.550        | 332373         |  5760				|
|SIDH CLN16 |
|alice 0   | 131668.375       | 123.081      | 302137162      |  282611			|
|bob       | 294733.750       |  98.261      | 676320830      |  225784			|
|alice 1   | 124323.111       | 110.163      | 285282463      |  253098			|
|LWE OKCN recommended |
|alice 0   | 1280.909         | 8.566        | 2939184        |  19638			|
|bob       | 1721.036         | 13.754       | 3949199        |  31491			|
|alice 1   | 122.716          | 2.449        | 281470         |  5528				|
|LWR OKCN recommended |
|alice 0   | 1104.251         | 7.091        | 2533816        |  16243			|
|bob       | 1673.630         | 12.146       | 3840346        |  27904			|
|alice 1   | 150.001          | 2.335        | 344097         |  5286				|


Contents
--------

liboqs currently contains:

- `kex_lwr_okcn` : "OKCN-LWR": key exchange from learning with rounding (LWR) in our paper
- `kex_lwe_okcn` : "OKCN-LWE": key exchange from learning with error (LWE) in our paper
- `kex_rlwe_bcns15`: key exchange from the ring learning with errors problem (Bos, Costello, Naehrig, Stebila, *IEEE Symposium on Security & Privacy 2015*, [https://eprint.iacr.org/2014/599](https://eprint.iacr.org/2014/599))
- `kex_rlwe_newhope`: "NewHope": key exchange from the ring learning with errors problem (Alkim, Ducas, Pöppelmann, Schwabe, *USENIX Security 2016*, [https://eprint.iacr.org/2015/1092](https://eprint.iacr.org/2015/1092)) (using the reference C implementation of NewHope from [https://github.com/tpoeppelmann/newhope](https://github.com/tpoeppelmann/newhope))
- `kex_rlwe_msrln16`: Microsoft Research implementation of Peikert's ring-LWE key exchange (Longa, Naehrig, *CANS 2016*, [https://eprint.iacr.org/2016/504](https://eprint.iacr.org/2016/504)) (based on the implementation of Alkim, Ducas, Pöppelmann, and Schwabe, with improvements from Longa and Naehrig, see [https://www.microsoft.com/en-us/research/project/lattice-cryptography-library/](https://www.microsoft.com/en-us/research/project/lattice-cryptography-library/))
- `kex_lwe_frodo`: "Frodo": key exchange from the learning with errors problem (Bos, Costello, Ducas, Mironov, Naehrig, Nikolaenko, Raghunathan, Stebila, *ACM Conference on Computer and Communications Security 2016*, [http://eprint.iacr.org/2016/659](http://eprint.iacr.org/2016/659))
- `kex_sidh_cln16`: key exchange from the supersingular isogeny Diffie-Hellman problem (Costello, Naehrig, Longa, *CRYPTO 2016*, [https://eprint.iacr.org/2016/413](https://eprint.iacr.org/2016/413)), using the implementation of Microsoft Research [https://www.microsoft.com/en-us/research/project/sidh-library/](https://www.microsoft.com/en-us/research/project/sidh-library/)

Building and Running
--------------------

We only provide version for Linux.

### Linux and macOS

To build, clone or download the source from GitHub, then simply type:

	make

This will generate:

- `liboqs.a`: A static library with implementations for the algorithms listed in "Contents" above.
- `test_rand`: A simple test harness for the random number generator.  This will test the distance of PRNG output from uniform using statistical distance.
- `test_kex`: A simple test harness for the default key exchange algorithm.  This will output key exchange messages; indicate whether the parties agree on the session key or not over a large number of trials; and measure the distance of the sessions keys from uniform using statistical distance.

To run the tests, simply type:

	make check

Documentation
-------------

Some source files contain inline Doxygen-formatted documentation.  The documentation can be generated by running:

	doxygen

This will generate the `docs/html` directory.

License
-------

liboqs is licensed under the MIT License; see [LICENSE.txt](https://github.com/open-quantum-safe/liboqs/blob/master/LICENSE.txt) for details.  liboqs includes some third party libraries or modules that are licensed differently; the corresponding subfolder contains the license that applies in that case.  In particular:

- `src/aes/aes.c`: public domain
- `src/kex_rlwe_bcns15`: public domain ([Unlicense](http://unlicense.org))
- `src/kex_rlwe_msrln16`: MIT License
- `src/kex_rlwe_msrln16/external`: public domain ([CC0](http://creativecommons.org/publicdomain/zero/1.0/))
- `src/kex_rlwe_newhope`: public domain
- `src/kex_sidh_cln16`: MIT License
- `src/rand_urandom_chacha20/external`: public domain
