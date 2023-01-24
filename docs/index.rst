.. Simstack documentation master file, created by
   sphinx-quickstart on Tue May  4 20:20:25 2021.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

Welcome to SimStack's documentation!
====================================   

.. figure:: assets/simstack-client-server.png

        The **SimStack** workflow framework is based on a client-server concept connected via SSH command.

Unlocking the secrets of materials through computational simulations is an exciting journey that brings together 
the knowledge of physics, materials science, chemistry, mechanical engineering, mathematics, and computer science. 
While new simulation methods can be time-consuming and require a deep understanding of physical and chemical 
concepts, a few key parameters are often enough to transfer an established protocol from pre-existing code to a 
slightly different problem. However, this transferability is only sometimes considered during the development 
phase. But don't worry! The **SimStack** workflow framework is here to help, making simulation protocols more 
reusable, reproducible, flexible, and transferable. This new way dramatically reduces the time and effort required 
to set up a new or existing workflow and simplifies the complexity of high-performance computing resources, 
enabling you to quickly prototype complex multiscale workflows for materials design in your scientific 
simulation solutions. Welcome to the wonderful world of **SimStack**!

We are excited to guide you through **SimStack**'s features in a selection of **WaNos** to build straightforward workflows 
and showcase the concepts of reusability, reproducibility, transferability, and flexibility that underpin the workflow 
philosophy by running our tutorials! Let's dive in!

.. toctree::
   :maxdepth: 1
   :caption:  Installation & Configuration

   installation/index
   installation/server

.. toctree::
   :maxdepth: 1
   :caption: Tutorials

   tutorials/projectile_motion/index
   tutorials/dft_graphite/index

.. toctree::
   :maxdepth: 1
   :caption: WaNos

   wanos/simulation_wanos/index
   wanos/auxiliary_wanos/index

.. toctree::
   :maxdepth: 1
   :caption: Development

   development/best_practices/index
   development/incorprating/index
   development/simstack_tags/index

.. toctree::
   :maxdepth: 1
   :caption: Contact & Citing

   contact_citing/contact/index
   contact_citing/citing/index
   contact_citing/dev_team/index


.. |date| date:: %b %d, %Y

This document was generated |date|.
