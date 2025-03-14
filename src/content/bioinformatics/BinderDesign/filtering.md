# backbones filtering


In *design binders via RFdiffusion and ProteinMPNN-FastRelax*, at the beginning of *sequence design and binder assessment script `mpnn_af.slm`*, we could perform a fitering step to remove useless backnones.

In my opinion, this is a very heloful step, because it greatly increase the speed and efficiency of desigining reasonable binders. For example, in my `target.pdb`, I only expect designed binders could bind with the outside part of the `target.pdb` (see fig.1).


<center>
  <figure>
    <img src=".\bioIMG\CB.PNG" alt=" " width="600">
    <figcaption>fig.1 `target.pdb` and atoms where binders should bind with</figcaption>
  </figure>
</center>





<center>
  <figure>
    <img src=".\bioIMG\vis_bbs.PNG" alt=" " width="600">
    <figcaption>fig.2 distribution of all designed backbone centers</figcaption>
  </figure>
</center>

