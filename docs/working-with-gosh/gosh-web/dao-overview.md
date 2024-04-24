
<!-- ### __Overview of the DAO__ -->


All information about your DAO and its activities will be displayed here.

![](../../images/gosh_web_Create_ORG_04_DAO-page.jpg)

Information about DAO assets is displayed on the right.

### **DAO total supply**  
the total issue of tokens of this DAO.

### **DAO reserve**  
unallocated tokens.

Push on the **Send** button, you will create an proposal to transfer tokens from the DAO reserve to the DAO member.
<!-- TODO -->

Push on the **Mint** button, you will [create an proposal to mint additional tokens](../gosh-web/working-with-tokens-and-karma.md#additional-minting-of-tokens-for-dao) for this DAO.

![](../../images/gosh_web_OVERVIEW_01_total_suply.jpg)


### **Your wallet balance**  
the amount of tokens you have in this DAO.

    !!! info
        When creating a DAO, 20 tokens from the DAO reserve will be issued to your wallet.

    Push on the **SEND** button, you will to transfer your tokens to the DAO reserve or to the GOSH user.
<!-- TODO -->

### **Karma**  
the amount of tokens (upper limit) within which a DAO member can vote. 

    It is assigned when accepted as a member of the DAO. This determines the reputation of the DAO member. The Karma can be changed only by voting.

![](../../images/gosh_web_OVERVIEW_02_wallet_balance.jpg)


### **Members**  
total number of DAO members.

    From here you can also send an invitation to become a member of the DAO.

<!-- TODO -->

![](../../images/gosh_web_OVERVIEW_03_members.jpg)


### **Recent proposals**

Information and status of the recent proposals will be displayed  in this section. 
Click on the name of the proposal you can go to the event page and [vote](../gosh-web/proposals-and-voting-in-smv.md#voting-procedure).

![](../../images/gosh_web_OVERVIEW_05_recent_proposals.jpg)


### **Repositories**  
In the **Repositories** section, you can quickly find or [create a repository](../gosh-web/repository.md#create-repository).

![](../../images/gosh_web_OVERVIEW_06_repositories.jpg)

### **DAO system repository**

The **_index** is a DAO system repository that is created automatically.

!!! info
    After creating the DAO, it will already contain 
    a text file with a brief description of your DAO,
    which you added in the settings earlier.

To add a README for your DAO, go to the _index repository or follow the link in this section.

<!-- and [create a file](../gosh-web/repository.md#create-file) in the main branch. -->
<!-- TODO
replace to create file -->

![](../../images/gosh_web_OVERVIEW_04_readme_md.jpg)

Make sure you are in the **main** branch and click **Add file** button.

![](../../images/gosh_web_Readme_md_01.jpg)

Enter file contents and name.

![](../../images/gosh_web_Readme_md_02_content.jpg)

You can use **Preview** if needed. MD syntax is supported for preview.

After scroll down and enter commit info:

* Commit description - you can add a description of your commit;

* Commit tags - this is a mutable pointer of the commit. You can add the tag to quickly go to this commit and see what has been done;

<!-- ![](../../images/gosh_web_Readme_md_03_data_commit.jpg) -->
![](../../images/gosh_web_Readme_md_03_2_data_commit.jpg)

* Select a task - if you want to attach your commit to the solution of the Task, then select the desired task from the list;

![](../../images/gosh_web_Task_11_select_tast.jpg)

* and add Assigners, Reviewers and Managers if necessary.

![](../../images/gosh_web_Task_11_2_select_tast_participants.jpg)

If a Task has been selected, check the **Create proposal** box.

And click **Commit changes**

![](../../images/gosh_web_Readme_md_03_data_commit.jpg)

<!-- ![](../../images/gosh_web_Readme_md_04_commit_prosess.jpg) -->

After that a proposal to the pull request will be created.

![](../../images/gosh_web_Task_12_proposal_to_commit_with_task.jpg)

When the proposal to the pull request is accepted, the description of the DAO will appear on the **Overview** tab.

![](../../images/gosh_web_Readme_md_05_owerviw.jpg)
