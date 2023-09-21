# Hands-on Workshop September 21, 2023

Please see the [Clusters Guide](../clusters_guide/) and other documentation sections on the left for more information.

Contact: Megan Duff and Jan Mandel will be happy to answer any questions!

[Zoom link for online support](https://olucdenver-my.sharepoint.com/:w:/g/personal/jan_mandel_ucdenver_edu/EfW7dw5ejYhOvaGY4GvdeUkB9OKWDeEcX05JiokcJUvw1Q?e=rNHemh)

## Log in
* know your CU Denver username
* open a Terminal (mac or linux), or command/powershell window (windows 10 or 11) 
* type into the window: *ssh your_username@math-alderaan.ucdenver.pvt* (replace *your_username* by your own username, of course)
* Enter your CU Denver password
    
## Check out the command line
* The easiest text editor is *nano*, exit it by *control-x*
* *mkdir* to make a directory, *cd* to change directory. *cd ..* will go to the parent directory.
* *man commandname* to get help about a command. Try *man top*

## Get the templates
* Type *git clone https://github.com/ccmucdenver/templates* 
* Type *cd templates* and *ls* to see what files you have there 

## Submit a batch job
* Look at the file *alderaan_simple.sh*
* Submit it: *sbatch alderaan_simple.sh*
* Look for the output file, it will have name starting with *slurm* 
* Try a GPU job: *sbatch alderaan_single_gpu.sh*  What did it do? Look at the output.

## Using multiple CPUs at the same time
* Multiple cores within a single node - just put the number on the --ntasks or -n line other than 1 when using software that written to use multiple cores automatically, such as R or Matlab.
* Multiple cores on multiple nodes - we have 2048 cores total on the compute nodes! - you need to have a code specifically written for this. Let's build some. Type 
    cd examples
    make
* Look at *alderaan_single.sh* *alderaan_mpi_general.sh* and submit them
* Look at *run_alderaan.slurm* and submit it. What is it doing?

## Singularity containers
* Complete computing environments with custom software and different Linux versions.
* Our containers are in */storage/singularity*. See [Singularity](../singularity/) for what containers we have and more details.
* *alderaan_single_gpu.sh* you used before runs tensorflow in a singularity container. Look at the script how it works!
* *singularity_alderaan_shell.slurm* allows you to run an entire shell script in a singularity container. Try to add another command. Try to use another container.
* **Extra credit:** run the examples from [https://github.com/ResearchComputing/Intro_GPU_Acceleration](https://github.com/ResearchComputing/Intro_GPU_Acceleration).

## Interactive jobs
* Please do not ssh to work on compute nodes, you could interfere with jobs running there which would make you very unpopular. It is OK to ssh to compute nodes to check on your running jobs submitted through sbatch, however.
* The magical incantation *srun -p math-alderaan --time=2:00:0 -n 1 --pty bash -i* will teleport your session to a compute node for two hours with one core reserved for you. Try it! Your interactive job will not interfere with CPU usage of other. Try *matlab -nodesktop*, run something CPU intensive, ssh to the node from another terminal window, and try *top* 

## Memory
* Our compute nodes have 64 cores and 512GB memory each. This seems like a lot, but you may be sharing it with others. We do not control memory as an allocatable resource yet, so if you need to use a large amount of memory, talk to us first.


