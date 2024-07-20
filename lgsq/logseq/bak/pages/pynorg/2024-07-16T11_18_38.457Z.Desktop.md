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
	- DONE *Purpose:* ((6666cdbd-301d-4ba5-b069-e43a105145e7)) | Implement re-indexing with caching as `.json`
	  :LOGBOOK:
	  CLOCK: [2024-06-10 Mon 13:51:47]--[2024-06-21 Fri 18:26:41] =>  268:34:54
	  CLOCK: [2024-06-21 Fri 18:29:14]--[2024-06-21 Fri 19:30:46] =>  01:01:32
	  :END:
		- DONE First iteration
		- CANCELLED Improve the multi-processing of ripgrep using [concurrent.futures](https://docs.python.org/3/library/concurrent.futures.html#concurrent.futures.ProcessPoolExecutor) module
		  :LOGBOOK:
		  CLOCK: [2024-06-10 Mon 13:55:52]
		  :END:
			- `multiprocessing.Process` performs comparably with `concurrent.futures`.
		- DONE Avoid linking to self
		  :LOGBOOK:
		  CLOCK: [2024-06-21 Fri 18:29:32]--[2024-06-21 Fri 19:30:45] =>  01:01:13
		  :END:
	- LATER *Purpose:* ((6666cdbd-301d-4ba5-b069-e43a105145e7)) | Implement metadata parsing of `.norg` files
	  :LOGBOOK:
	  CLOCK: [2024-06-10 Mon 13:51:50]
	  :END:
		- DONE First iteration as a helper function
		- LATER Improve parsing to be able to consistently extract all fields (including "categories")
	- TODO [#A] *Purpose:* ((6666cdbd-301d-4ba5-b069-e43a105145e7)) | Fix issue with multiple backlinks to same file
- # Notes
	- **Rationale for using `ripgrep`/`rg`**
		- *here*