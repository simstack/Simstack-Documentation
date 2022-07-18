.. Simstack documentation master file, created by
   sphinx-quickstart on Tue May  4 20:20:25 2021.
   You can adapt this file completely to your liking, but it should at least
   contain the root `toctree` directive.

Welcome to SimStack's documentation!
====================================

.. note::
   Documentation including tutorials are maintained in a joint project by Nanomatch and KIT.
   We are happy to receive your questions or comments at info@nanomatch.de or simstack@int.kit.edu

.. figure:: assets/simstack-client-server.png

        The **SimStack** workflow framework is based on a client-server concept connected via SSH command.

Understanding the nature of the materials from a computation simulation perspective
evolves fields that bring together knowledge from physics, materials science, chemistry,
mechanical engineering, mathematics, and computer science. While new simulation methods
are time-consuming and require in-depth knowledge about the physical/chemical ideas, a
few key parameters typically suffice to transfer an established protocol from pre-existing
code with a given method to a slightly different problem. However, this transfer is often
not accounted for during the development phase. The **SimStack** workflow framework handles
this drawback by enhancing the reusability, reproducibility, flexibility, and transferability
of simulation protocols. Those advantages reduce the time-consuming to setup an old or new
workflow hiding the complexity of high-performance computing (HPC) resources, enabling users
to perform rapid prototyping complex multiscale workflows for materials design into
their scientific simulation solutions.

This documentation will demonstrate how to apply the **SimStack** features in a predefined
set of **WaNos** to construct simple workflows to illustrate the reusability, reproducibility,
transferability, and flexibility concepts within the workflow philosophy.

.. toctree::
   :maxdepth: 1
   :caption:  Installation & Configuration

   installation/index
   installation/server

.. toctree::
   :maxdepth: 1
   :caption: Tutorials

   tutorials/projectile_motion/index

.. toctree::
   :maxdepth: 1
   :caption: Development

   development/best_practices/index
   development/incorprating/index
   development/simstack_tags/index


.. |date| date:: %b %d, %Y

This document was generated |date|.
