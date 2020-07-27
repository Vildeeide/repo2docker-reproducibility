# Reproducibility with repo2docker 


Code reproducibility is key to realize the potential of the open science paradigm. The present project focuses on literate programming using Jupyter Notebooks. The work is inspired by Pimentel et al's "A large-scale study about quality and reproducibility of jupyter notebooks", and more specifically the seventh research question of the paper; "How reproducible are notebooks?". 

To explore this question, the project focuses on the Jupyter tool repo2docker, as well as public repositories accessed through GitHub. In short, repo2docker fetches a given code repository and builds an environment in which the code can be executed. Thus, theoretically, the tool facilitates reproducibility and moves open science closer to its goal. However, due to the lack of cross-language standard practices for environment specifications, it was hypothesized that the idea behind repo2docker is better than its actual performance. Consequently, this project explores the potential of efficient code reproducibility using repo2docker.

The project was divided into three broad work tasks: Exploring, testing, and comparing. During the first stage, repositories were manually sampled from GitHub. Popularity and relevance to machine learning were the main sampling criteria. The repositories were used by repo2docker to test the tools' performance. The results of the building of images were analyzed and classified to get a picture of the common failures of repo2docker. As was hypothesized to be a general trend, a large group of the sample failed to build due to a mismatch between frozen dependencies and the version of Python specified. 

Next to Python notebooks, it is important to note that the sample also included notebooks written in R and Julia to also cover languages without clear common practices regarding environment specifications. 

Repo2docker is used by BinderHub, which builds images on demand and stores data about all binders that run each day in an event archive. To test repositories that have been used by Binder, and therefore are likely to build with repo2docker, we tested repo2docker with the 20 most popular repositories from the event archive as a second sample of repositories. Also these repositories resulted in build failures, and based on the results we continued to the next stage of the project. 

Although repo2docker is a tool with potential, there are no existing automatic tools that predict whether it will succeed. The motivation to develop such a tool, named repo2docker-checker, raised as a consequence of the high failure rate of repo2docker. The checker executes at most five notebooks found in a given repository, before it returns the results, including the execution failures if relevant. In addition to the limitation of restricting the number of notebooks to test to five, this approach assumes that the answer to the question of whether execution is a reasonable test is yes. Future research should explore this, as it is possible that execution is not the best way to predict repo2docker's performance. 

As the last stage of the testing of repo2docker-checker, repositories were sampled from the work by Pimentel et al. Based on the different classifications of the repositories from their database, we could compare the performance of repo2docker-checker to the results of Pimentel et al. 

The results of the comparison support the initial concern that many environments are specified with pinned dependencies and no specified Python version. This can be seen by looking at the percentage of notebook execution failures that arise as a consequence of modules that are being called in the notebooks, but not being found, which on average is 60.4%, with a maximum of 93.3%. Furthermore, out of all repositories that were tested with repo2docker-checker, very few had notebooks that could be run without any errors (average of 15%). 

These results are interesting as they underline the high failure rate of repo2docker, and they give insight into the reason for the failures. One can see from this that although repo2docker motivates specification of dependencies, authors of code fail to do so. Additionally, from our analyses, it became evident that strict package pinning caused more failures than loose pinning. 

Furthermore, looking at the performance of R and Julia repositories, our analysis shows that R and Julia communities do not appear to adopt the “existing community best practices” for specifying environments. In general, there was a very low rate of kernel presence. With better practices within these communities, code reproducibility is likely to get closer to its potential.

Our analysis also show that the success rate of repo2docker is closely related to the Python version that is specified. Although the Python community specifies requirements in a way that repo2docker understands, the lack of Python version specification results in low success rate. Furthermore, the latest version of Python which is used by repo2docker as a default creates a high failure rate. Future work should look at alternative ways of picking the right Python version, such as retrieving information from notebook metadata or using the publishing date of the repository.


To conclude, code reproducibility plays an important role in the open science paradigm, and Jupyter's tool repo2docker is a step towards realizing the reproducibility potential. However, this project has shown that the failure rate of the tool is high, mainly due to a mismatch between pinned dependencies and unspecified Python versions. Building on the work of Pimentel et al, repo2docker-checker was developed to automatically predict repo2docker's performance. This project gives insight into the potential of repo2docker and highlights areas of change and improvement. 

#### Conclusion highlights:
- Strict pinning of dependencies without pinning the Python version is widespread and bad, resulting in a low success rate for repo2docker.
- Strict package pinning caused more failures than loose pinning.
- R and Julia communities do not appear to adopt our "existing community best practices" for specifying environments, which is seen by a very low rate of kernel presence at all.
- The Python community specifies requirements in way repo2docker understands, but not the Python version (low success rate). By default, the latest Python version is chosen, and results in a high failure rate compared to other methodologies. Different strategies for picking default Python could increase success rate.


#### References:
###### Pimentel, J. F., Murta, L., Braganholo, V., & Freire, J. (2019, May). A large-scale study about quality and reproducibility of jupyter notebooks. In 2019 IEEE/ACM 16th International Conference on Mining Software Repositories (MSR) (pp. 507-517). IEEE.

###### MyBinder Event Archive. https://mybinder-sre.readthedocs.io/en/latest/analytics/events-archive.html. Retrieved 15/07/2020. 

###### Repo2docker Documentation. https://repo2docker.readthedocs.io/en/latest/. Retrieved 20/07/2020.

