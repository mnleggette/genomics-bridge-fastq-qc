Sequencing Data Quality Assessment | Genomics Bridge 01
Project type: Self-directed bioinformatics training · Platform: Galaxy · Software: FastQC 0.12.1
Research question
What quality issues are present in the raw sequencing reads from the female_oral2.fastq-4143.gz sample used in the Galaxy Training Network quality-control tutorial, and what should be investigated before downstream microbial analysis?
Dataset and method
- Sample: female_oral2.fastq-4143.gz (snake oral microbiome tutorial dataset). Biological context is based on the tutorial, not inferred from the sequence alone.
- Source: Galaxy Training Network, Quality Control tutorial. Dataset hosted at Zenodo record 3977236.
- Analysis: Imported compressed FASTQ into Galaxy USA, ran FastQC with default settings, and inspected HTML report and raw FastQC output. No trimming or filtering was performed.
- Reproducibility: Original FastQC HTML, raw results and summary are supplied in fastqc_outputs/.
Basic statistics
Metric	FastQC result
Total sequences	812
Total bases	240.3 kbp
Read length	296 bases
GC content	44%
Sequences flagged as poor quality	0
Quality encoding	Sanger / Illumina 1.9


Important: “0 sequences flagged as poor quality” is a field in FastQC basic statistics; it does not mean all bases or reads passed all QC modules.
Findings
1. Per-base sequence quality — FAIL
Per-base mean Phred quality was Q37.72 at base 1, remained about Q36.71 at bases 100–104, then dropped to Q29.56 at bases 105–109 and Q15.61 at bases 295–296. Read-end deterioration and increasing variability suggest that some later base calls may be unreliable. This does not imply every read has uniformly low quality.

2. Per-sequence quality scores — WARNING
The mean-read-quality distribution is bimodal, with major peaks at Q21 (236 reads) and Q37 (141 reads); another 136 reads are at Q20. An earlier informal visual estimate of a single Q30–Q34 peak was incorrect. This split warrants consideration of distinct quality subpopulations, without assigning a cause on FastQC evidence alone.

3. Adapter Content — FAIL
The adapter module detects a Nextera Transposase Sequence signal reaching 54.56% and poly-A reaching 47.54% at later reported positions. Poly-G and the three listed Illumina adapter categories remain at 0% in the recorded table. The Nextera-associated signal is a recognized adapter-category match, but the FastQC report alone does not establish its experimental origin or the best trimming parameters. Earlier visual labeling of this plot as poly-A plus poly-G was incorrect and was corrected against raw FastQC data.

4. Additional QC checks
The report also flags per-base sequence content (FAIL), per-sequence GC content (FAIL), sequence duplication levels (FAIL), and overrepresented sequences (FAIL). Per-tile sequence quality is WARNING. The duplication summary lists a 36.82% estimated deduplicated fraction (per FastQC's method). An overrepresented prefix beginning GTGTCAGCCGCCGCGG... occurs in 46 reads (5.67%); the FastQC Possible Source field is No Hit. In targeted amplicon/microbiome workflows, unusual composition and duplication can sometimes be expected, so these flags require protocol-aware interpretation.

Conclusion and next steps
This initial untrimmed dataset shows substantial late-cycle loss of base-call quality plus Nextera-associated sequence detection and poly-A signal. Do not treat the reads as unequivocally ready for biological inference without reviewing the sequencing/library-preparation protocol. Examine whether primer/adapter trimming and quality-based trimming or filtering are appropriate; document settings, rerun FastQC after any preprocessing, compare retained read lengths and QC metrics, and only then proceed to microbial classification or other downstream analysis.
Limitations
Single input dataset; 812 reads. The analysis uses FastQC summary metrics and graphs only, without independent taxonomic assignment, known experimental metadata verification, or before/after trimming comparison. Module failures indicate QC flags rather than proof that all reads are unusable. No claim is made about the identities of organisms in the sample.
Teach-back video outline (5–7 minutes)
1. Question: “Before studying the snake oral microbiome, can I trust the sequencing reads?”
2. FASTQ discovery: Explain four-line records and why G in the quality line is encoded Q38 rather than guanine.
3. Prediction and first test: Show per-base Q falling toward read ends.
4. Unexpected finding: Contrast the two mean-read-quality peaks (Q21 and Q37).
5. Research correction: Explain how raw data corrected the mistaken poly-G interpretation to Nextera transposase + poly-A. Treat verification as a positive scientific practice.
6. Decision: Discuss why trimming requires protocol review and a follow-up QC comparison.
What I Learned: My First Genomics QC Project 🧬
Going into this project, I knew I wanted to learn genomic sequencing and analysis, become more profieicnt in the softwares, but I didn't fully understand what working with actual sequencing data would look like. I knew DNA was made up of A's, T's, C's, and G's, but what exactly was I supposed to do with all those letters once they were sitting in front of me on a computer screen?

Wellllll, turns out there's a whole lot that happens before you can even begin answering the biological questions. 😂

One of my earliest assumptions was about the long stretches of repeating A's and G's I noticed in the FASTQ file. I initially wondered whether AAAAAAAA or GGGGGGGG meant a codon was somehow switched on or off, or whether those repetitions were telling me something about gene activity.

Turns out, I was asking a completely different biological question from what the data could actually answer!

I learned that a codon is a sequence of three nucleotides that specifies an amino acid or translation stop signal in the appropriate coding context. A codon isn't simply switched on or off. Gene expression and gene regulation involve additional biological processes, and repeated nucleotides alone don't establish whether a gene is active or inactive.

I also learned that context matters enormously. Repeating A's in the DNA-sequence line may represent a poly-A stretch, while repeating G's in the quality-score line don't represent guanine at all! In that context, G is a character encoding a Phred quality score of Q38.

That distinction really changed how I looked at the file. The same letters can communicate entirely different information depending on where they appear and how the data is formatted.

Then came FastQC.

At first, I was simply looking at graphs with green checks, orange warnings, and red failures. But as I worked through the results, I started understanding that quality control isn't just about getting everything to turn green. It's about asking why something was flagged, what the data actually shows, and what information I still need before making a decision.

Another important learning moment was realizing that my initial interpretation of the Adapter Content graph wasn't quite right. I thought I was seeing poly-A and poly-G patterns, but after examining the raw results, I learned that one of the prominent signals was associated with a Nextera sequencing adapter. That reminded me that scientific interpretation requires more than looking at a graph and making an assumption.

And honestly, that's what I enjoyed most about this project: learning how to ask better questions.

I started with a FASTQ file that looked like an overwhelming collection of letters and symbols. By the end, I had used Galaxy and FastQC to investigate sequencing quality, interpret Phred scores, recognize potential technical artifacts, and make preliminary recommendations for further analysis.

I'm also realizing how important it is to understand the biology behind the data. So, alongside my genomics training, I'm planning to brush up on genetics and biochemistry. I want to understand more about DNA structure, nucleotide chemistry, codons, gene regulation, mutations, and the molecular processes involved in sequencing—not just how to interpret a graph, but why the patterns I'm seeing might occur in the first place.

My goal is to bring greater depth and breadth to both my written report and video teach-back by connecting what I'm learning in bioinformatics to the underlying genetics, biochemistry, and biological processes.

I also want these projects to reflect my curiosity as a developing researcher. I'm interested in more than learning a particular software tool or completing a workflow. I want to explore how different scientific disciplines inform one another, investigate questions that emerge from my findings, and develop the background knowledge to interpret those findings more thoughtfully.

For me, demonstrating depth means understanding the scientific reasoning behind my analysis. Demonstrating breadth means being able to make meaningful connections across genetics, molecular biology, biochemistry, and computational methods. And demonstrating curiosity means being willing to follow a question beyond the original assignment, even when that means returning to the fundamentals to learn something new.

I'm hoping that approach will make my reports more scientifically meaningful and my teach-back videos more engaging, while documenting how my knowledge and research skills develop over time.

I'm still very much learning, and this is only my first step into bioinformatics. I haven't identified the microorganisms in this sample or completed downstream sequencing analysis yet.

But I understand something now that I didn't when I started: before I can confidently explain what the biology is telling me, I need to understand the quality of the data telling the story.

And THAT is pretty cool. 🧬🤎
Repository contents
- README.md — documented analysis and discussion
- figures/ — selected unaltered FastQC figures
- fastqc_outputs/ — downloaded HTML report, raw QC results and module summary
This is an educational analysis, not a claim of experimentally validated species identification.
