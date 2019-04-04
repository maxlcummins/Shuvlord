configfile:
    "config/snake-shovill.config.json"

sample_ids, = glob_wildcards(config['reads']+"/{sample}_R1.fastq.gz")


print(sample_ids,)

rule all:
    input:
        expand("assemblies/{sample}.out", sample=sample_ids),
        expand("final_assemblies/{sample}.out/{sample}.fasta", sample=sample_ids)


rule shovill:
    input:
        r1 = config['reads']+"/{sample}_R1.fastq.gz",
        r2 = config['reads']+"/{sample}_R2.fastq.gz"
    output:      
        directory("assemblies/{sample}.out")
    conda:
        "config/shovill.yaml"
    shell:
        """
        shovill --minlen 200 --outdir {output} --R1 {input.r1} --R2 {input.r2}
        """

rule rename:
    input:
        "assemblies/{sample}.out"
    output:
        "final_assemblies/{sample}.out/{sample}.fasta"
    shell:
        "mv {input}/contigs.fa {output}"

