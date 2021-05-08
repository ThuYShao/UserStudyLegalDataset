# UserStudyLegalDataset

Dataset for SIGIR'21 paper: ***Investigating User Behavior in Legal Case Retrieval***. 

## Dataset Description

The dataset contains three parts:

- **Query Cases** ("query_case.json").  The designed tasks in our user study. The example format:

  ```json
  [ -- All tasks
    { -- One task
      "task_id": 1, 
      "category": "criminal", -- criminal/administrative/civil
      "difficulty": "hard", -- designed task difficulty, hard/easy
      "query_case_description": "被告人张某为练习自己的炒股技能....",
   		"Causes": ["非法侵入计算机信息系统罪", "故意毁坏财物罪"], -- Cause of Action
    },
    ...
  ]
  ```

  

- **User Behavior Log** ("page_log.json").  We logged user behavior on the search result pages (SERPs) and the landing pages (LDpages) in our user study, including queries, click-through, hovering, scrolling, and dwell time. The file contains logs on both types of pages. The keys might differ a bit according the page type (i.e., SERP or LDpage). The example format:

  ```json
  { -- One log record
    "user_id": 0,
    "user_field": "none",  -- User legal specialty, criminal/administrative/civil/none,
    "task_id": 1,
    "page_oid": "5ea41aef1d30fd787958a6b5", -- the object id in the database
    "start_timestamp": 1587812967206,
    "end_timestamp": 1587813103447,
    "dwell_time": 62592,
    "view_height": 760, -- in px, the visible height of the page
    "page_timestamps": "[{\"inT\": 1587812967206, \"outT\": 1587813014689}...]", -- a stringfy list, each item indicates the time get in/out of the page
    "ptype": "SERP", --page type, SERP - Search Result Page, LDPage_PTAL/LDPage_QWAL - Landing Page of common/authoritative case
    "query_str": "[{\"id\":-1,\"text\":\"全部\"},{\"id\":0,\"text\":\"职务侵占\"}]", -- query items, a stringfy list, only available on SERPs
    "cause_all": [], -- the Causes in the query, annoted mannually after the study, only available on SERPs
    "cause_correct": [], -- the correct Causes, annoted mannually after the study, only available on SERPs
    "formulation_type": "SUB", -- type of query reformulation, INT - initial query, GEN - generalization, SPE - specification, SUB -- substitution,
    "cases": "[...]", -- a stringfy list. For SERP, it contains html contents of each result item (e.g., snippets). For LDPage, it contains the html contents of the case shown to the user. 
    "clicked_results": "[{\"id\": 0, \"case_id\": \"1833AA6CFC9D4AEF21CC0418F374B7D0\", \"case_type\": \"authoritative_case\", \"timeStamps\": 1587813014400, \"refer\": \"5ea41ae51d30fd787958a6b4\"}, ...]" -- a stringfy list, if a user clicked on a case result, the record would be formatted as this examaple. id - the rank of case in the result list. case_id - the object id of the case of the search engine. case_type - common/authoritative case. timeStamps - the timestamps of click. refer - the "page_oid" of the clicked page.
    "hover_results": "[{\"id\": 0, \"case_type\": \"PTAL\", \"hover_in\": 1587812971932, \"hover_out\": 1587813001512}, ...]" -- a stringfy list, only available on SERP. If a user hovered on a case result, the record would be formatted as this example. id - the rank of case in the result list. case_type - PTAL/QWAL, same as common/authoritative case. hover_in - the timestamp of starting hovering. hover_out - the timestamp of ending hovering. 
  	"scrolls": "[{\"Sx\": 0, \"Sy\": 5, \"St\": 1587813000374, \"Ex\": 0, \"Ey\": 95, \"Et\": 1587813000507, \"Ty\": \"scroll\"},...]", -- a stringfy list. Each item is a scrolling record. Sx/Ex - the Starting/Ending horizontal position, Sy/Ey - the Starting/Ending vertical position. St/Et - the timestmap of Starting/Ending scrolling. Always, Sx=Ex=0, Ty=scroll.
  	"moves": "[{\"Sx\": 819, \"Sy\": 322, \"St\": 1587813000112, \"Ex\": 817, \"Ey\": 327, \"Et\": 1587813000300, \"Ty\": \"move\"},...]", -- a stringfy list. Each item is a mouse-moving record. Sx/Ex/Sy/Ey/St/Et are similiar with those of scrolls. Always, Ty=move.
  	"referrer": "5ea41aef1d30fd787958a6b5", -- a page_oid or a null string. If this page is accessed from the other page, the referrer indicate the corresponding page's page_oid. 
  } 
  ```

  

- **Candidate Case Details** ("case_details.json"). The detailed information of the case on the LDpage, including the cleaned case text, the case structure, the section position, and annotations. The example format:

  ```json
  { -- One case
    "user_id": 0,
   	"task_id": 1,
   	"page_oid": "5ea41ae51d30fd787958a6b4", -- the object id in the database
   	"cid": 0, -- case id on the page
   	"case_type": "QWAL", -- QWAL/PTAL, same as common/authoritative case
   	"case_info": [
   		{
   			"p_title": "当事人信息", -- the section title
   			"p_content": "...", -- the content in this section
   			"ptop": 300, in px, the abosution top postion of this section,
   			"pheight": 198.0, in px, the height of this section
  		}, ...
   ], -- a list of sections
  	"mark_timestamp": 1587813276789, -- the timestamp of bookmarking. -1 (the default value) indicates that the case was not bookmarked.
  	"relevance_user": 3, -- the user annotated relevance, only available in bookmarked cases.
  	"relevance_label": 1, -- the relevance assessed by external experts, only available in bookmarked cases.
  	"reason_text": "...", -- the reasons for the relevance score given by the user.
  }
  ```



## How to get the dataset?

We provide example data (i.e., examples/ )to help researchers have a quick start. For the A) the whole dataset or 2) the implementation of the user study platform / browser extension, please contact [Yunqiu Shao](shaoyunqiu14@gmail.com) . For more details, please refer to our paper [Investigating User Behavior in Legal Case Retrieval](http://www.thuir.cn/group/~YQLiu/publications/SIGIR2021Shao.pdf) . If you  have any questions, please email [Yunqiu Shao](shaoyunqiu14@gmail.com). 



## Citation

If you use the dataset in your research, please add the following bibtext citation in your references. 

```
@inproceedings{shao2021investigating,
 author = {Shao, Yunqiu and Wu, Yueyue and Liu, Yiqun and Mao, Jiaxin and Zhang, Min and Ma, Shaoping},
 title = {Investigating User Behavior in Legal Case Retrieval},
 booktitle = {Proceedings of the 44th International ACM SIGIR Conference on Research and Development in Information Retrieval},
 series = {SIGIR'21},
 year = {2021},
 location = {Virtual Event, Canada},
 publisher = {ACM},
} 
```

