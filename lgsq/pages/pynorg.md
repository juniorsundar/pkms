link:: https://www.github.com/juniorsundar/pynorg

- # Tasks
	- DONE Create basic Python project repository
	  :LOGBOOK:
	  CLOCK: [2024-06-10 Mon 13:51:41]--[2024-06-10 Mon 13:51:42] =>  00:00:01
	  :END:
	- DONE Implement CLI base tooling
	  :LOGBOOK:
	  CLOCK: [2024-06-10 Mon 13:51:44]--[2024-06-10 Mon 13:51:45] =>  00:00:01
	  :END:
	- DOING *Purpose:* ((6666cdbd-301d-4ba5-b069-e43a105145e7)) | Implement re-indexing with caching as `.json`
	  :LOGBOOK:
	  CLOCK: [2024-06-10 Mon 13:51:47]
	  :END:
		- DONE First iteration
		- DOING Improve the multi-processing of ripgrep using [concurrent.futures](https://docs.python.org/3/library/concurrent.futures.html#concurrent.futures.ProcessPoolExecutor) module
		  :LOGBOOK:
		  CLOCK: [2024-06-10 Mon 13:55:52]
		  :END:
	- DOING *Purpose:* ((6666cdbd-301d-4ba5-b069-e43a105145e7)) | Implement metadata parsing of `.norg` files
	  :LOGBOOK:
	  CLOCK: [2024-06-10 Mon 13:51:50]
	  :END:
		- DONE First iteration as a helper function
		- TODO Improve parsing to be able to consistently extract all fields (including "categories")
- # Notes
	- **Rationale for using `ripgrep`/`rg`**
		- *here*