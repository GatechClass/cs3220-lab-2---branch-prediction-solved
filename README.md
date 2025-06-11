# cs3220-lab-2---branch-prediction-solved
**TO GET THIS SOLUTION VISIT:** [CS3220 Lab #2 – Branch Prediction Solved](https://mantutor.com/product/cs3220-lab-2-branch-prediction-solved-2/)


---

**For Custom/Order Solutions:** **Email:** mantutorcodes@gmail.com  

*We deliver quick, professional, and affordable assignment help.*

---

<h2>Description</h2>



<div class="kk-star-ratings kksr-auto kksr-align-center kksr-valign-top" data-payload="{&quot;align&quot;:&quot;center&quot;,&quot;id&quot;:&quot;113812&quot;,&quot;slug&quot;:&quot;default&quot;,&quot;valign&quot;:&quot;top&quot;,&quot;ignore&quot;:&quot;&quot;,&quot;reference&quot;:&quot;auto&quot;,&quot;class&quot;:&quot;&quot;,&quot;count&quot;:&quot;2&quot;,&quot;legendonly&quot;:&quot;&quot;,&quot;readonly&quot;:&quot;&quot;,&quot;score&quot;:&quot;5&quot;,&quot;starsonly&quot;:&quot;&quot;,&quot;best&quot;:&quot;5&quot;,&quot;gap&quot;:&quot;4&quot;,&quot;greet&quot;:&quot;Rate this product&quot;,&quot;legend&quot;:&quot;5\/5 - (2 votes)&quot;,&quot;size&quot;:&quot;24&quot;,&quot;title&quot;:&quot;CS3220 Lab #2 - Branch Prediction Solved&quot;,&quot;width&quot;:&quot;138&quot;,&quot;_legend&quot;:&quot;{score}\/{best} - ({count} {votes})&quot;,&quot;font_factor&quot;:&quot;1.25&quot;}">

<div class="kksr-stars">

<div class="kksr-stars-inactive">
            <div class="kksr-star" data-star="1" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" data-star="2" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" data-star="3" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" data-star="4" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" data-star="5" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
    </div>

<div class="kksr-stars-active" style="width: 138px;">
            <div class="kksr-star" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
            <div class="kksr-star" style="padding-right: 4px">


<div class="kksr-icon" style="width: 24px; height: 24px;"></div>
        </div>
    </div>
</div>


<div class="kksr-legend" style="font-size: 19.2px;">
            5/5 - (2 votes)    </div>
    </div>
Part 1: Baseline Branch Predictor: 50 pts

Part 2: Performance Measurement &amp; Optimization: 50 pts + 10 bonus pts (overflow allowed)

Submission ddl: Feb 17th

Part 1: Baseline Branch Predictor (50 points):

In this part, you’ll be implementing a baseline branch predictor and a branch target buffer for your RISC-V CPU. Here’s a concise overview of the design:

1. The branch history register (BHR) has a length of 8 bits, you will use PC[9:2] XOR BHR to index a Pattern History Table (PHT).

3. The PHT is composed of 2^8 2-bit counters to make branch prediction. Each counter is initialized with 1 (indicating a weakly not taken).

4. The branch target buffer (BTB) has 16 entries, and you will use PC[5:2] to index it. Each entry of the BTB is composed of 3 parts: a valid bit, a tag field, and a target address:

5. the tag field is used to determine whether the current PC address in the FE stage is the one recorded in the BTB entry;

6. the valid bit is used to identify whether this entry contains a valid history, rather than unused;

7. the target address is used to predict the branch / jump target.

Summary of the G-share branch prediction algorithm:

FE Stage (fe_stage.v):

Both BTB and PHT are concurrently accessed in this stage.

1. If there’s a BTB hit, use PHT outcome to determine the target address for the next instruction fetch: if the outcome is taken, use BTB target address. If BTB misses, use PC+4 for next instruction.

2. The address for the next instruction fetch and index (PC[9:2] XOR BHR) used in FE stage is passed to EX stage for PHT update.

EX stage (agex_stage.v):

1. Check if the next instruction fecthed in the FE stage is correct or not: if not, flush the pipeline.

2. If the branch is taken, and the next instruction we fetched is not the branch target, we are supposed flush the pipeline;

3. If the branch is not taken, and the next instruction we fetched is not PC+4, we should flush the pipeline.

4. For branch instructions (bne, beq, jalr, etc.), insert the target address into the BTB, no matter taken or not.

5. If PHT is used for branching prediction in the FE stage, update PHT using the propagated PHT index (PC[9:2] XOR BHR).

6. Update the BHR.

7. As BHR and PHT are implemented in the FE stage, you are supposed to forward the relevant signals to the FE stage for the updates mentioned in 2, 3 and 4 via from_AGEX_to_FE.

To pass earn full credit of this part, implement the baseline branch predictor described above and make sure your baseline branch predictor passes testall.mem and all testcases under part2.

Grading: We will check the testcases are correctly executed or not.

There wonâ€™t be any performance improvement in testall.mem because the branch should always be predicted to not taken, since each branch instruction is executed only once (the branch predictor only works if you encounter same instruction multiple times).

This testcase is only intend to test that the branch predictor you implement is not distructive for the other functionalities of the RISC-V processor.

Part 2: Performance Measurement &amp; Optimization (50 points + 10 bonus pts)

1. [40 pts] For this part, you will evaluate branch prediction accuracy by adding counters to measure it (# of correctly predicted branches / # total branch instructions). Utilize the towers.mem testcase for this assessment and write your measurement results in a pdf report.

2. Note that jump instructions should be counted as branch instructions here as well.

4. To gain credits from part-2, your baseline predictor should have &gt; 30% accuracy.

5. [10 pts + 10 pts bonus] Enhance the performance of your branch predictor on the towers.mem testcase by making design changes: you can explore other BHR hashing functions (e.g. using different bits of PC for the XOR operation), or change the PHT or BTB sizes. Implement at least three different design changes, and present the corresponding performance outcomes in your report. If your modifications result in more than a 5% increase in prediction accuracy compared to the baseline branch predictor, you will earn 10 bonus points.

Submission

Provide a zip file containing your source code for Part 1. Generate the submission.zip file using the command make submit. Avoid manual zip file creation to prevent any issues with the autograding script, which could lead to a 30% score deduction.

Submit a concise PDF report for Part 2 (limited to 2 pages) containing the following information:

Your performance measurements for the baseline G-share branch predictor and your three variants.

Discuss the design parameters that were modified and explain how these changes influenced branch prediction accuracy, either positively or negatively.

Do not put this pdf inside the zip file.

No need to submit code for Part 2.

FAQ

[Q] I passed testall.mem but failed to pass some testcases under test/part2. What should I do? [A] Please carefully check whether your when-toflush logic is correctly implemented in the AGEX stage based on the following criteria:

If the branch is taken, and the next instruction we fetched is not the branch target, we are supposed flush the pipeline;

If the branch is not taken, and the next instruction we fetched is not PC+4, we should flush the pipeline as well

[Q] Iâ€™m debugging my code. I see that there is an X in the BTB. How would it be possible? [A] FE stage can have pipeline bubbles. Therefore, BTB/BHT might be indexed with uninitialized values. Please make sure when you update BTB/BHT, only branch instructions/signals (not including X) can change the BTB/BHT values.

[Q] I donâ€™t see performance improvement in testall.mem. Why? [A] This is expected. All branch code in testall.mem are executed only once and not-taken. In order to make a branch predictor work, the processor has to see the same branch over and over. W/o training, the branch predictor wouldâ€™t work well.

[Q] Do we insert a BTB entry only for the taken branch or even when it is not taken? [A] You need to insert a BTB entry even the branch is not taken. Because the same branch might be taken in the next time.

[Q] If we insert a not-taken branch for the BTB entry, what will be the target address? [A] You can still compute the target address as if it is taken and insert it in the BTB.

[Q] What if the target in the BTB is wrong? [A] Just like a branch misprediction, we flush the pipeline and also update the BTB with the correct information.

[Q] With a branch predictor, will the pipeline still have pipeline bubbles? [A] The pipeline will have pipeline bubble for dependency stalls but not for branch instructions.

[Q] I want to add a new file (bp.v). can I? [A] Please do not add new file, as it might break our auto-grading script.

[Q] Do I have to show the performance improvement in order to get a full-credit for part 1? [A] No. the performance improvement needs to be demonstrated in part 2 only.

[Q] Are we expected to implement data forwarding in lab 2? [A] No.

[Q] Letâ€™s say my instruction stream is as follows: BR(1) ADD BR(2) . When BR(1) is in EX, it will update the BHR. But BR(2) will be in FE at that time. Which value of BHR should FE use? The old value or the updated value from EX? [A] This is one of the optimization opportunities. So how you handle this case is up to you. Please remember that the branch predictor is just a predictor and it won’t affect the correctness of the program.

[Q] How to initialize PHT as one? [A] You should explicitly put 1s when it resets.

[Q] I ran tower.mem and my test case is failed unlike other test cases. Is that expected? [A] Yes. The tower.mem returns “255”, which does not match the PASS criteria of the simulator. You do not need to worry about it.
