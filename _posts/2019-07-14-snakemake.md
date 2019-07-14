---
layout: post
title: Snakemake
subtitle: Creating workflows with Snakemake
published: false
---

A note about automation: There are a lot of automation workflows that I'm just starting to use. Snakemake was introduced to me while teaching at the [ANGUS workshops](LINK HERE), and I'm still incorporating them into my workflow. I hope this helps you figure them out - they can be a little tricky but are well worth the time investment! 

When you first learn about putting programs together (i.e. making a pipeline), you're generally taking the lines of code you put straight into the command line and putting them into a text file, and then you make it executable (`chmod +x <script.sh>`). Then you run it like this `bash script.sh` or like this `./script.sh`. Your computer then reads the file beginning to end, working through each line and using variables in a fairly straightforward way. 
![](/img/bashworkflow.png)

This works just fine, so why would you want to automate your workflow with snakemake? 
 * If you make a mistake in part of your script after you've aleady executed it, you'll probably kill the job and fix the error, and then rerun everything. For the type of research I do, this becomes time-consuming really fast because the initial steps take a while. Snakemake is able to tell whether a part of your workflow has been completed and doesn't rerun it if it's already finished. I'll talk about how it does this, but it's easily my favorite reason to use snakemake. 
 * Easy to read workflow. Bash scripts can get really complex, and if you're still figuring out variables and file names, the paths to your files or scripts in your code can overwhelm useful information
 * Reproducibility. Certain features of snakemake, like the incorporation of conda, make it easier to send your whole workflow to a colleague and have them run it on their machine of choice with your data with the same software you used! 

 If you're convinced, let's get started. 
 Compared to the bash workflow up above, this is what a workflow looks like in snakemake: 

![](/img/bashworkflow.png)

So what's going on here? Notice first that the steps are now called rules. Each rule dicatates a separate part of your workflow. Instead of the flow going from beginning to end like in your shell script, snakemake is going to start with the end product of your workflow (in this case the output from `samtools_index`) and then work it's way back up your pipeline. If one rule doesn't have all it needs to run