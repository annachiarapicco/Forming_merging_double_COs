# Forming_merging_double_COs
From the paper Forming merging double compact objects with stable mass transfer (A. Picco et al. (2024)) [![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.10955659.svg)](https://doi.org/10.5281/zenodo.10955659). I am still adjusting this, for any questions text me at annachiara.picco@kuleuven.be. 
By now I am providing the following:

1. **HE-MS folder**
   
   This is the working directory with which I produced the Helium Zero Age Main Sequence (He-ZAMS) models, with initial masses $0.275 M_{\odot} ≤ m_{\mathrm{d,f}} ≤ 52.75 M_{\odot}$, where $m_{\mathrm{d,f}}$ is the donor star's mass at the end of the stable MT episode. I explain this in the last paragraph of Sec. 2.5 of the paper. The working directory works with MESA v15140.
   
3. **BOUNDARIES folder**
   
    This contains my semi-analytical calculations for the instability boundary (Sec. 2.3) and merging time boundary (Sec. 2.1), based on the mass-radius exponents grid provided by Ge et al. (2020) for donor star's initial masses $2 M_{\odot} ≤ m_{\mathrm{d,i}} ≤ 100 M_{\odot}$. The subfolders are named by the donor star's initial mass value, and inside the subfolders you will find txt files called in this fashion: `Info_{M}Msun_upsi{upsilon}.txt`, where `M` is the donor star's mass, and upsilon is the efficiency $\upsilon$ of L2 outflow as defined in Sec. 2.6. The upsilon value in the name of the files just mean that some (not all!) information inside the file is related to the relevant upsilon. Normally, there should be four possible values of upsilon: $\upsilon=1.0,0.75,0.5,0.25$. Should you need a particular value, drop me a message 🌝 The file has many columns, some of which are just for visualization purposes. The important ones are:
   - 🔴 **_INSTABILITY BOUNDARY_**, $\beta=1$
     
     This is the "red solid" line you see in Fig. 5 of the paper, for example. It represents the instability (or common envelope, CE) boundary derived in the fully isotropic re-emission ($\beta=1$, if you look into Eq.4 or Eq. 19) limit. For this boundary, you have:
      1. `logP0_crit`: initial period, in $\log P_{\mathrm{i}}$ (days), at which the unstable MT episode is initiated.
      2. `m1iso_crit`: mass of the accretor at which the unstable MT episode is initiated. This is the same at the start of the MT and at the end, since $\beta=1$ implies no accretion.
      3. `phases_crit`: index, along the arrays of `logP0_crit` and `m1iso_crit`, at which TAMS, core He ignition and core He depletion are found. These are directly derived from Get et al. (2020) simulations, as they provide the central abundances in their grid.
      4. `m2iso_crit`: mass of the donor star at the end of the MT episode; calculated with a stripping factor derived from Ge et al. (2020) in the way described in Sec. 2.4, more specifically Eq. 17.
   
   - 🔵 **_TIME DELAY BOUNDARY_**, $\beta=1$
     
     This is the "indigo solid" line you see in Fig. 5 of the paper, for example. It represents the boundary for systems that have post-MT properties leading to a GW merger, i.e. with time delay $t_{\mathrm{merge}}< 13.8$ Gyr. The shrinkage of the orbit is calculated in the isotropic re-emission ($\beta=1$) limit, Eq. 8. For this boundary, you have:
      1. `logP0_hub`: initial period, in $\log P_{\mathrm{i}}$ (days), to which the maximum accretor mass `m1iso_hub` for GW mergers after the MT episode is corresponding.
      2. `m1iso_hub`: maximum initial (and final) mass of the accretor at which you find GW mergers after the MT episode.
      3. `phases_hub`: index, along the arrays of `logP0_hub` and `m1iso_hub`, at which TAMS, core He ignition and core He depletion are found. These are calculated by comparing the phases_crit with equi-Roche-Lobe loci in the $\log P_{\mathrm{i}} -m_{\mathrm{a,i}}$ diagram.
   
   - ⚪️ **_ROCHE LOBE BOUNDARY_** $\beta=1$
     
     This is the "solid gray" line you see in Fig. 5 of the paper, for example. It represents the boundary that we imposed to have sensible orbital separations, at the end of the MT episode, such that the post-MT donor star would still fit into its own Roche Lobe, see Sec. 2.5. For this boundary, you have:
      1. `logP0_RHeRL`: initial period, in $\log P_{\mathrm{i}}$ (days), to which the maximum accretor mass `m1iso_RHeRL` for the orbit to fit a Zero Age Main Sequence Helium star after the MT episode is corresponding.
      2. `m1iso_RHeRL`: maximum initial (and final) mass of the accretor at which you find post MT properties suitable to fit a  Zero Age Main Sequence Helium star within its own Roche Lobe.
      3. `m2iso_RHeRL`: mass of the donor star at the end of the MT episode, corresponding to the `logP0_RHeRL` and `m1iso_RHeRL` initial properties. These are found by interpolating within the provided stripping factor from Ge et al. (2020), the corresponding equi-Roche-Lobe loci and the radii of the Zero Age Helium Main Sequence stars models.
   
   - **_HR DIAGRAM OF MODELS_**
     
     Just for completeness, you find the columns of `logL_Lsun` and `logTeff` at which the models in the Ge et al. (2020) grid are starting their adiabatic mass loss episode.

   - **_THE upsilon>0 BOUNDARIES_**
     
     These are the instability ("dashed red" line of Fig. 5), time delay ("dashed blue" line in Fig. 5) and Roche Lobe ("dashed gray" line in Fig. 5) boundaries in the case in which the MT has some L2 outflow efficiency upsilon equal to the value printed in the name of the file. The MT episode is still assumed to be completely non-conservative, by setting $\beta+\upsilon=1$, see Eq. 19 and paragraph 2.6. The names of the relevant columns follow exactly the same notation as the ones described above:
      1. 🔴 Instability boundary: (`logP0_critL2_DEF`, `m1iso_critL2_DEF`)
      2. 🔵 Time delay boundary: (`logP0_hubL2_DEF`, `m1iso_hubL2_DEF`)
      3. ⚪️ Roche Lobe boundary: (`logP0_RHeRLL2_DEF`, `m1iso_RHeRLL2_DEF`)
         
     **NB**: You might notice that there are some columns that are called like the ones listed here above, but without the `"_DEF"` in the end. These are not used in the paper and concern a different fitting function to the L2 position, rather than the "definitive" (hence, DEF) one, in Eq. 20. Just stick to these.

    - **_NEUTRON STAR PROGENITORS_**: $8 M_{\odot} < m_{\mathrm{d,i}} < 20 M_{\odot}$
      
      For these objects, I am still providing all the information above, which holds in the case of direct collapse fate after the MT episode. To account for the possible occurrence of supernova kicks, I also computed distributions of post supernova properties as explained in Sec. 3.2. I have grids (to be uploaded soon) for these, that can produce the data for the colormap of a plot like the one in Fig. 8. For the sake of illustrations, I am providing in the `Info_{M}Msun_upsi{upsilon}.txt` file the following additional three columns:
      1. `logP0_PmergeMIN`
      2. `m1iso_PmergeMIN`
      3. `m2iso_PmergeMIN`

      These are following the same notation as seen above, and they are mapping an iso-contour of probability $P_{\mathrm{merge}}$ of merging within 13.8 Gyr such that $P_{\mathrm{merge}}=0.1$ (the "dashed black line" in Fig. 8, for example). This is derived in the fully isotropic re-emission limit, $\beta=1$.



_COMING SOON_: 
1. Boundaries for $\epsilon>0$ with $\epsilon=1+\beta$ and $\beta = 0.,0.5,1.$ . See Sec. 3.5 of the paper, in which I discuss the effect of including some conservativeness.
2. Overview txt files with the $\zeta_{\mathrm{ad}}$ and $q_{\mathrm{crit}}$ in the conservative approximation, as read by Ge et al. (2020) tables directly.
3. Grids for NS progenitors kicks, so that the user can compute the iso-contours of fixed $P_{\mathrm{merge}}$ probabilities.
4. Plotting / visualization scripts used in the paper.
