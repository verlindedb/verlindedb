---
title: "Conventions and General Information"
math: true
---
# TL;DR
- Use the table in the homepage to find a category
  - Searching and sorting by various data is available
- On the category page, hover over a fusion product, \\(S\\) matrix entry, or twist factor to see what produces it
- All tables of fusion rules and \\(S\\) matrices are given in lower triangular form. One can use symmetry of both to get the upper triangle
- You can copy the .tex source of the fusion tables and \\(S\\)-matrices, which is useful if the browser cannot render them reasonably quickly
# Background 
All categories appearing on this site are known as Verlinde modular categories. A concise reference for these categories is Section 5 of Galindo, Mora, Rowell "Braided Zestings of Verlinde Modular Categories and Their Modular Data"[^2]. A more detailed construction is Bakalov and Kirillov Jr.'s book[^1]. This site is inspired by the [AnyonWiki](https://anyonwiki.github.io). While the goal of this site is slightly different, the spirit is identical. For one thing, the former presents a novel contribution to the understanding of fusion rings.

All data presented on this site are generated using SageMath's [FusionRing class](https://doc.sagemath.org/html/en/reference/algebras/sage/algebras/fusion_rings/fusion_ring.html#sage.algebras.fusion_rings.fusion_ring.FusionRing). In principle, one can generate their own database containing the same data, but no one-stop reference exists in a publicly available location as far as the author knows. As such, this is merely a subset of a collection of existing information, limited by the practicality of displaying high rank fusion tables and S matrices on a webpage.

The choices of which root systems and levels to add here is somewhat of an arbitrary decision. 
It is largely capped by how much time I am willing to let the page generation process run. In particular, the \\(S\\)-matrix generation is quite slow for some categories, especially for \\(E_n\\) and \\(F_4\\). One might say these take an exceptional amount of time.
The second bottleneck is the limitation of the browser DOM to reasonably load and display so many elements.
As you might have already noticed, as the rank increases, so does the render time for the tables and matrices.
On my browser, that limit is around rank 40. As such, most Verlinde categories under rank 40 are presented here. 
 
# Conventions Used
- The monoidal unit of the category will always have label \\(1\\).
- All simple objects are given a numeric label, ordered by Frobenius-Perron dimension (low to high)
- Numeric Frobenius-Perron dimensions are truncated to 3 decimal places
- When a fusion rule has multiplicity, the object appearing \\(n\\) times in a direct sum will be written \\(n \cdot X\\), where \\(X\\) is the simple object
- \\(\zeta_n\\) denotes a primitive \\(n\\)th root of unity
- A twist factor is a rational number \\(h\\) such that the ribbon twist of a simple object \\(X\\) is \\(\theta_X = \exp( \pi i h)\\)
- Frobenius-Perron dimensions are simplified to the extent that SageMath can simplify them
- All tables of fusion rules and \\(S\\) matrices are given in lower triangular form. One can use symmetry of both to get the upper triangle
- The central charge \\(c\\) is a rational number such that 
\\[
D_+ / D_{-} = \exp(\pi i c/2 )
\\]
where \\(D_{\pm}\\) are the positive and negative Gauss sums
\\[
D_\pm = \sum_{X\text{ simple  }} \theta^{\pm 1 }_X \operatorname{dim}(X)^2.
\\]
# Construction and Notation of Verlinde Modular Categories
We cover the construction and notation of the first reference. We assume general familiarity with fusion categories. Let \\(\mathfrak{g}\\) denote a simple Lie algebra and \\(h^\vee\\) denote the dual Coxeter number of \\(\mathfrak{g}\\). A Verlinde category is constructed out of the category of representations of the quantized universal enveloping algebra \\(U_q(\mathfrak{g})\\) where \\(q\\) is a root of unity parameter.

Specifically, one takes the *tilting* representations of \\(U_q(\mathfrak{g})\\) and semisimplifies it at a positive integer *level* \\(k\\)[^1]. When one chooses a level \\(k\\) and an associated Cartan type for \\(\mathfrak{g}\\), the quantization parameter is given by 
\\[
q = \exp\left({\frac{\pi i}{m(k + h^\vee)}}\right\).
\\]
Denote the constructed category as \\(\mathcal{C}(\mathfrak{g},k)\\).
Below is a table summarizing the choices and associated categories as well as the notation used on this site[^2].

<center>

| Cartan Type | \\(\mathfrak{g}\\) | \\(q = \exp\left({\frac{\pi i}{m(k + h^\vee)}}\right\)\\) |\\(\mathcal{C}(\mathfrak{g},k)\\) |
| :---: | :---: | :---: | :---: |
| \\(A_n\\) | \\(\mathfrak{sl}_{n+1}\\) |\\(\exp\left({\frac{\pi i}{n+1+k}}\right\)\\) |\\(\operatorname{SU}(n+1)_k\\) |
| \\(B_n\\) | \\(\mathfrak{so}_{2n+1}\\) |\\(\exp\left({\frac{\pi i}{2(2n-1+k)}}\right\)\\) |\\(\operatorname{SO}(2n+1)_k\\) |
| \\(C_n\\) | \\(\mathfrak{sp}_{n}\\) |\\(\exp\left({\frac{\pi i}{2(n+1+k)}}\right\)\\) |\\(\operatorname{Sp}(n)_k\\) |
| \\(D_n\\) | \\(\mathfrak{so}_{n}\\) |\\(\exp\left({\frac{\pi i}{2n-2+k}}\right\)\\) |\\(\operatorname{SO}(2n)_k\\) |
| \\(E_6\\) | \\(\mathfrak{e}_{6}\\) |\\(\exp\left({\frac{\pi i}{12+k}}\right\)\\) |\\(\operatorname{E}_6(k)\\) |   
| \\(E_7\\) | \\(\mathfrak{e}_{7}\\) |\\(\exp\left({\frac{\pi i}{18+k}}\right\)\\) |\\(\operatorname{E}_7(k)\\) |
| \\(E_8\\) | \\(\mathfrak{e}_{8}\\) |\\(\exp\left({\frac{\pi i}{30+k}}\right\)\\) |\\(\operatorname{E}_8(k)\\) |
| \\(G_2\\) | \\(\mathfrak{g}_{2}\\) |\\(\exp\left({\frac{\pi i}{3(4+k)}}\right\)\\) |\\(\operatorname{G}_2(k)\\) |
| \\(F_4\\) | \\(\mathfrak{f}_{4}\\) |\\(\exp\left({\frac{\pi i}{2(9+k)}}\right\)\\) |\\(\operatorname{F}_4(k)\\) |

</center>

In terms of the fundamental weights, one can parameterize everything there is to know about these categories, including the modular data.
This opens the door for computer-assisted generation of the data of these categories, which is done in SageMath.



 

[^1]: Bakalov & Kirillov (2000-11-20) Lectures on Tensor Categories and Modular Functors, American Mathematical Society.
[^2]: Galindo, Mora & Rowell (2024-10-07) Braided Zestings of Verlinde Modular Categories and Their Modular Data, Communications in Mathematical Physics.


