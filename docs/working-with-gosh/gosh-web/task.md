<!-- 
## __Working with Task__ -->



### __Create Task__


To create a Task, go to the Tasks tab and click **Create Task**

![](../../images/gosh_web_Create_Task_01.jpg)

Then you need to fill in the Task conditions.

The result of the Task should be a pull request to include changes in the repository.

Select the repository for which the Task is being created.

![](../../images/gosh_web_Task_02_fill_repo.jpg)

Add the Task name.

You can add 3 tags separated by spaces to quickly find the task.

![](../../images/gosh_web_Task_03_name_tags.jpg)

Then you need to evaluate the Task.

**Task cost** is the number of tokens that will be paid from the DAO reserve for its execution.

!!! info
    The members of the DAO agree between themselves how to evaluate the Tasks.

After attaching a pull request to the Task, the tokens will be distributed between the author, reviewer and manager in the ratio you set.

**Commit author** - the person who executes the Task.  
**Reviewer** - the person who checks the correctness of the Task.  
**Manager** - the person who manages the Task execution process.

!!! info
    The number of authors, areviewers and managers is set at your choice.  

![](../../images/gosh_web_Task_04_cost_distrb.jpg)

Select vesting and lock periods. 

**Lock (cliff)** - the period after which the reward payments will begin. 
The countdown will start after accepting the proposal about completing the Task.  
**Vesting** - rules for transferring the fixed part of the tokens to the disposal of the contractor.

For example, lock - 12 months, vesting - 2 months.  

!!! warning
    In order for the investment scheme to be correct, the smaller of the number of tokens allocated to the members of the task must be a multiple of the number of months of investment.

![](../../images/gosh_web_Task_05_lock_vesting.jpg)

Add a comment the token distribution rules and click **Create task and start proposal**

![](../../images/gosh_web_Task_06_comment.jpg)

After creating the proposal, you will be taken to the **DAO** tab with events.

![](../../images/gosh_web_Task_07_event.jpg)

Inside the proposal you will be able to see all the conditions of the Task.  
In the table you can see the period since which month and in what parts the payments will be made to the members of the Task.

<!-- ![](../../images/gosh_web_Task_08_proposal.jpg) -->

![](../../images/gosh_web_Task_09_event_details.jpg)

After accepting the proposal, the Task will appear in the list on the **Tasks** tab with the status *Awaiting commits*.

!!! info
    When creating a Task the tokens (Task cost) from the DAO-reserve are written off and reserved on the Task-contract.

![](../../images/gosh_web_Task_10_list_tasks.jpg)

When the Author has completed the Task, he adds it to the commit.

!!! info
    If you need to make several commits to complete a Task,, create a separate branch.  

And do **Select task** when creating the proposal to the pull request.

Select the Task performed(s), reviewer(s), manager(s) if they worked on the task. The allocated shares of those who were not specified will be returned to the DAO-reserve.

![](../../images/gosh_web_Readme_md_03_data_commit.jpg)

After that a proposal to the pull request will be created.  

![](../../images/gosh_web_Task_12_proposal_to_commit_with_task.jpg)

Detailed information can be viewed by going to it on the DAO tab with events.

![](../../images/gosh_web_Task_13_detail_proposal.jpg)

If the reviewer was specified during the commit, the event will wait for verification from them.

![](../../images/gosh_web_Task_14_event%20review.jpg)

Then, after the reviewer send the solution, it will be possible to vote for the proposal.  
When the pull request is accepted, the Task status will change to **Confirmed**.

![](../../images/gosh_web_Task_15_task_status_confirmed.jpg)

After the lock period ends, the members of the Task can receive a reward.
To do this, go to the **Tasks** tab in the completed Task and click **Claim reward**.

!!! note
    If Lock period (cliff) has been set to zero, then you can click **Claim reward** immediately after accepting the pull request.

![](../../images/gosh_web_Task_16_claim_reward.jpg)

Thus the tokens will begin to be transferred to the wallets of the members of the completed Task in accordance with the vesting scheme when the lock period ends.


### __Deletе Task__


To delete a Task, go to it on the **Tasks** tab.
And click to **Delete task**

![](../../images/gosh_web_Task_delete_01.jpg)

After creating a proposal about deleting a Task, you will be redirected to the event tab **Dao**.

![](../../images/gosh_web_Task_delete_02_event.jpg)

When the proposal is accepted, the Task will be deleted.  
The tokens allocated for this Task will be returned to the DAO reserve.

