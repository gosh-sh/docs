

<!-- ## __Working with Repository__ -->



### __Create Repository__


To create a repository in your DAO click **Create new** in the Repositories section or Overview section.​

![](../../images/gosh_web_Create_Repo_01_new_repo.jpg)

Enter repository name and its description and click **Create repository**.

!!! warning
    The repository name must contain only Latin letters, numbers,hyphen, underscore character`( a...z, 0...9, -, _ )`

![](../../images/gosh_web_Create_Repo_02_name_repo.jpg)

A page with **DAO** events will open for you.

![](../../images/gosh_web_Create_Repo_03_event_create_repo.jpg)

Open the event click on its name.

![](../../images/gosh_web_Event_02_all.jpg)

The page that opens displays the name of the proposal, its status, and the time of creation and as well as the end of voting.

![](../../images/gosh_web_Event_03_status_time_details.jpg)

The scale shows the number of votes for the proposal and against.

![](../../images/gosh_web_Event_04_result.jpg)

Specify the number of tokens less than or equal to your Karma for voting and accept or reject this proposal.

Add your opinion about the proposal to the discussion below and click **Send vote**

![](../../images/gosh_web_Event_05_vote.jpg)

The created repository will appear in the list on the Repositories tab.

![](../../images/gosh_web_Create_Repo_04_repo_created.jpg)


#### __create repository with Expert Tags__

This will provide every Tag holder with increased Karma Powers when voting on commits, and for branch protection and unprotection.



### __​Create Branch__


Repository is created with default main branch. To create another branch, click on the **branches** counter.​

![](../../images/gosh_web_Create_branch_01.jpg)


Select the branch to be forked, enter new branch name, and click​ **Create branch**.

!!! warning
    The branch name must contain only Latin letters, numbers, hyphen, underscore character `( a...z, 0...9, -, _ )`

![](../../images/gosh_web_Create_branch_02_name.jpg)

Once the branch is created, it will appear in the branches list.

![](../../images/gosh_web_Create_branch_03_list_dranches.jpg)

Switch to it via drop down list.

![](../../images/gosh_web_Create_branch_04_switch_branches.jpg)


### __Create File__


To create file, click **Add file** button.

![](../../images/gosh_web_Create_file_01_new_file.jpg)

Enter file contents and name.

![](../../images/gosh_web_Create_file_02_name_contents.jpg)

You can use **Preview** if needed. MD syntax is supported for preview.

After scroll down and enter commit info:

* Commit description - you can add a description of your commit;

* Commit tags - this is a mutable pointer of the commit. You can add the tag to quickly go to this commit and see what has been done;

* Select task - if the branch is not protected and your file is a solution to a problem, you can choose a particular task;

* and add Assigners, Reviewers and Managers if necessary.


 and click **Commit changes**

![](../../images/gosh_web_Create_file_03_commit_data.jpg)

If the branch you are working in requires no voting to confirm commits, the file will be added. Otherwise a DAO [vote](../gosh-web.md#proposals-and-voting-in-smv-soft-majority-vote) will be initiated.

<!-- TODO
If the branch is protect -->

Commit status will be displayed below.

![](../../images/gosh_web_Create_file_04_proces_create_file.jpg)


### __Create Pull Request__


Click on the **Pull requests** tab and set up the pull request: what branch to merge from and to. Once selected, click **Compare**.

![](../../images/gosh_web_Create_PR_01.jpg)

The branches will be compared. Review the changes, set up the pull request and click Commit changes.

![](../../images/gosh_web_Create_PR_02_comparing.jpg)


!!! info
    **Note**: When merging into the main branch, and in some other cases (depending on DAO setup), a DAO proposal will be initiated by trying to commit.

    Organization Tokens have to be sent to the DAO Soft Majority Vote contract to start a proposal for DAO members to [vote](../gosh-web.md#proposals-and-voting-in-smv-soft-majority-vote) on.


### __Add protection for a branch__


If you want the changes to be added to the branch based on the voting results, then add protection to the branch.

This can be done by creating an appropriate proposal.

To do this, go from the **Repositories** tab to the repository you need.

![](../../images/gosh_web_Protect_branch_01_repos.jpg)

Then, on the Branches tab, click the **Protect** button for the branch to which you want to add protection.

![](../../images/gosh_web_Protect_branch_02_branches.jpg)

After creating the proposal, you will be redirected to the **DAO** page with events.

![](../../images/gosh_web_Protect_branch_03_events.jpg)

Inside the event, you can get details of proposal.

![](../../images/gosh_web_Protect_branch_04_details_proposal.jpg)

After the proposal is accepted the branch is marked as protected.  
A commit can be made to it only by voting.

![](../../images/gosh_web_Protect_branch_05_branches_protect.jpg)

### __Remove protection for a branch__

If the branch no longer needs protection, you can remove it by initiating appropriate proposals.

To do this, go from the **Repositories** tab to the repository you need.

![](../../images/gosh_web_Protect_branch_01_repos.jpg)

Then, on the Branches tab, click the **Unprotect** button for the branch to which you want to add protection.

![](../../images/gosh_web_Protect_branch_remove_01_branches.jpg)

A vote will be created and you will be redirected to the **DAO** page with events.

![](../../images/gosh_web_Protect_branch_remove_02_event.jpg)

Inside the event, you can get details of proposal.

![](../../images/gosh_web_Protect_branch_remove_03_details_proposal.jpg)

After accepting the proposal, the protection mark will be removed from the branch.  
Now everyone can upload changes to the branch without voting.

![](../../images/gosh_web_Protect_branch_remove_04_branch_unprotect.jpg)


### __Adding comments to file__

You can add a comment to any line in the file.

!!! info
    Comments are linked to a specific comment.


To do this, open the file and hover over a line or block of lines and click on the blue icon that appears on the left.

In the window that opens, enter your comment and click on the blue circle with an arrow to send it.

![](../../images/gosh_web_Comments_01.jpg)

The comment line will be marked with a red icon on the left.

![](../../images/gosh_web_Comments_02.jpg)

A thread of comments and replies to them will open on the right.

![](../../images/gosh_web_Comments_03.jpg)

The discussion can be resolved. To do this, click the appropriate button:

![](../../images/gosh_web_Comments_04_resolve.jpg)

!!! info
    The discussion can be resumed if a new comment has been added to it.

Up to 3 discussions can be expanded in one line.
You can switch between them.

![](../../images/gosh_web_Comments_05_more_comments.jpg)


### __Adding comments to Pull Request__

You can also add comments to Pull Request.
To do this, go from the **DAO** events page to the **Pull Request** vote in the **Pull request diff** section.
you can leave comments on any line or block of lines in the same way as in [commenting on a file](../gosh-web.md#adding-comments-to-file).

![](../../images/gosh_web_Comments_06_for_PR.jpg)
