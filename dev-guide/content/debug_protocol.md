# Expected Debugging Protocol [WIP]

1. Track the failure.
   1. Save one's work and the current state of the system. Check in the saved state via git with a descriptive message using the following format "[Bug] Insert 73-character-or-less bug description here."
   2. Create a github issue that documents the bug's existence. This will be a bug report containing:
      - A one line description of the problem. Should basically be the same as the message from the previous step.
      - A written description of the failure. What happened, in words?
      - A written description of the expected behavior. What was supposed to happen, in words?
      - Severity categorization: {Blocker; Major - aka large problem; Minor - aka an easy to fix problem; Enhancement - aka not a requirement but nice to have.}
      - A minimal working example or set of steps that reproduces the failure.
      - If possible (but not required now), a simplified test example that produces the same qualitative failure.
      - Any diagnostic information (errors, execution logs, etc.) reported when the failure was observed.
      - Environment information when the failure was observed (installed packages, operating system, memory capacity, etc.)
   3. Create a new branch off the feature branch to track work on fixing the bug.
   4. Open a pull request for the new branch to the original feature branch. Register that the issue is being worked on in this pull request by referencing the issue for the bug in the text body of the pull request on github.
   5. Add a test to the suite of regression tests to reproduce this specific software failure instance. Check the test in with git.
      - See chapter 4, "Reproducing Problems" of "Why Programs Fail: A Guide to Systematic Debugging" by Morgan Kaufmann.
   6. Create an automated and simplified test case for this specific failure instance.
      - See chapter 5, "Simplifying Problems" of "Why Programs Fail: A Guide to Systematic Debugging" by Morgan Kaufmann.

2. Understand how the system that is producing the failure is supposed to work.
   1. Identify and read the basic documentation related to the (relevant?) external software tools being used at or around the point of failure.
   2. Take basic trainings (e.g. online tutorials, online courses, etc.) in the external tools being used in your project.
   3. Identify, store, and read the details about major / complex algorithms that one's software is implementing.

3. Understand how the system that is producing the failure is working.
   1. What is being produced during failure?

      Ensure that one has a debugging system in-place to identify and record the intermediate values being produced by one's software as well as which of those values are incorrect in the simplest created test case.

   2. When does failure occur?

      If failure is intermittent or conditional, document what inputs, if any, cause the failure to occur rather than not.

   3. Where is the defective code?
      1. Hypothesize and record possible points where the bug could have been introduced.
      2. Be sure to include logically likely contributors to the failure's existence (e.g. other known bugs, causes in program state / code / input, anomolies in the output or intermediate variables, poorly written code, etc.).
      3. For each of those hypothesized points, determine whether the point is defective.
      4. For each defective point, determine whether that point actually changes the failure behavior.
      5. Employ various brute-force / common search techniques to discover remaining causes of the failure. [WIP--to be detailed.]
      6. Open a new task on the failure's github issue for each discovered contributor to the failure's existence (i.e.  each defect).
      7. Check out a new branch off of the bug-fixing branch for each discovered contributor to the failure's existence (i.e.  each defect).
      18. On the defect-fixing branch, create and check-in a test to document the defect's existence.
      19. Push each new branch to github and open a corresponding new pull-request (PR) for each discovered contributor to the failure's existence (i.e.  each defect). In the defect-fixing PRs, reference the failure's github issue, the test for the defect, and give a concise description of the defect.

    4. Why is the code defective?
       1. For each code defect identified above, hypothesize why the code is defective and record these hypotheses on the defect-fixing PR.
       2. Perform experiments to test one's hypotheses about the cause of the defect.
       3. Record the confirmed causes of the defect in the PR for the defect.
3. Fix the  failure.

   From the beginning of the chain of causation/computation to the end, isolate and fix each instance of defective code.

   1. For each defect being corrected, predict how a given change will (i) fix the specific failure case and (ii) fix the underlying cause of the defective code. Record these prediction in the defect's PR.
   2. Make a given change and test whether or not the defect is corrected.
   3. For each corrected defect, check whether the original failure is corrected by running the corresponding regression test.
   4. For each corrected defect, check whether any new problems are introduced by running the full test suite to ensure no new tests fail.
   5. For each corrected defect, check whether any similar defects exist in other parts of the code due to the same flawed reasoning that caused this defect.
   6. Close the PR for each corrected defect.
   7. Once the failure is fixed, check in the fix to git with a descriptive message following the format "[Bug-Fix] Insert 69-character-or-less description here."
   8. Merge the pull request to track that the bug was fixed and incorporate the changes.
