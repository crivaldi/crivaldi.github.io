---
layout: post
title: Snakemake
subtitle: Creating workflows with Snakemake
published: false
bigimg: /img/snakemake.png
---


<center><h3>A note about automation</h3></center>
<blockquote>
There are a lot of automation workflows that I'm just starting to use. Snakemake was introduced to me while teaching at the [ANGUS workshops](https://angus.readthedocs.io/en/2019/snakemake_for_automation.html), and I'm still incorporating them into my workflow. I hope this helps you figure them out - they can be a little tricky but are well worth the time investment! 
</blockquote>

## Why Snakemake?

When you first learn about putting programs together (i.e. making a pipeline), you're generally taking the lines of code you put straight into the command line and putting them into a text file, and then you make it executable (`chmod +x <script.sh>`). Then you run it like this `bash script.sh` or like this `./script.sh`. Your computer then reads the file beginning to end, working through each line and using variables in a fairly straightforward way. This is a shell script, or a bash script (if you're working in bash, which I generally do).
![](/img/bashworkflow.png)

This works just fine, so why would you want to automate your workflow with snakemake? 
 * If you make a mistake in part of your script after you've aleady executed it, you'll probably kill the job and fix the error, and then rerun everything. For the type of research I do, this becomes time-consuming really fast because the initial steps take a while. Snakemake is able to tell whether a part of your workflow has been completed and doesn't rerun it if it's already finished. I'll talk about how it does this, but it's easily my favorite reason to use snakemake. 
 * Easy to read workflow. Bash scripts can get really complex, and if you're still figuring out variables and file names, the paths to your files or scripts in your code can overwhelm useful information
 * Reproducibility. Certain features of snakemake, like the incorporation of conda, make it easier to send your whole workflow to a colleague and have them run it on their machine of choice with your data with the same software you used! 

 If you're convinced, let's get started. 

 ## How does Snakemake work? 

 Compared to the bash workflow up above, this is what a workflow looks like in snakemake: 

![](/img/snakemakeworkflow.png)

So what's going on here? Notice first that the steps are now rules. I used 'step' as an arbitrary word for the shell script, but rules are the functional units of snakemake workflows. Each rule dicatates a separate part of your workflow. Instead of the flow going from beginning to end like in your shell script, snakemake is going to start with the end product of your workflow (in this case the output from `samtools_index`) and then work it's way back up your pipeline. If one rule doesn't have all it needs to run, snakemake will keep tracing it's way back through the rules until it can start running. 

### What does a rule need to run? 

Most rules have an input, an output, and a shell line. There are more things you can add to a rule, but we'll keep it simple for now. 
 * The **shell** is where you put whatever command you would type into the command line. It's where you put the executable part of this step. You can have multiple shell commands.
 * The **output** is what files are coming out of your shell command. An example is an SAM file from a program like [bwa](http://bio-bwa.sourceforge.net/). You can have multiple outputs. You do not need to list all the output files your shell command might produce.
 * The **input** is the file (or files) coming in to the shell command. Examples are data (like a genome fasta) or a file that was the output of another step in your workflow (like an indexed genome). You can have multiple inputs.

 The rule will need whatever your shell command needs to produce the output. So if your input is a file that is also the output of an upstream rule, snakemake will keep looking through your rules until it finds that file. This is what it means when people describe snakemakea as working backwards - it starts with the final output of your workflow and keeps going up the chain until it finds the input of the rule in your first step. Let's see what this looks like with an example: 
 ```
rule bwa_index_reference:
    input: "mapping/orf_coding.fasta"
    output: "mapping/orf_coding.fasta.fai"
    shell:'''
    bwa index {input}
    '''
 ```  
The exact command I'm using here doesn't matter as much as the syntax I'm showing you. One **very important** note about writing snakemake rules is that you have to be really careful with spacing. This is because snakemake uses python syntax, and interprets those tabs and spaces as part of the code. Some languages (like bash) don't care about indents, so this can be tricky if you're not used to it. 
