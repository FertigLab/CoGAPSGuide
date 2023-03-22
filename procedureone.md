---

hero_image: /CoGAPS/images/hero.jpg
<!-- hero_height: is-fullwidth -->
hero_darken: true

---

# Running PyCoGAPS

## User startup guide for the Python CoGAPS API

We provide two options for running PyCoGAPS (Options A and B). Option A demonstrates running PyCoGAPS as a package in a Python script with an IDE, and Option B demonstrates automatic deployment and running NMF using a Docker image. Both options are functionally equivalent, so the user’s choice of interface should depend on factors such as familiarity with Python and desire for flexibility and modification. Option A provides a full walkthrough of PyCoGAPS package functions. However, to deploy and run PyCoGAPS in fewer steps with limited flexibility, we recommend following Option B. Please refer to Fig. 4 and/or Table 1 to determine which option is most appropriate to follow.

## Figure 4

![Decision Tree](images/decisiontree.png)

## Table 1


|                                        |                                                       |                         **Workflow Comparison**                        |                                      |                                                                                        |
|----------------------------------------|-------------------------------------------------------|:----------------------------------------------------------------------:|--------------------------------------|----------------------------------------------------------------------------------------|
| **Procedure Choice**                   | **Procedure 1:  PyCoGAPS**                            |                                                                        | **Procedure 2:  CoGAPS**             | **Procedure 3:  GenePattern Notebook**                                                 |
| **Option Choice**                      | **Option A:  Python scripts**                         | **Option B:  Docker**                                                  | --                                   | --                                                                                     |
| **Overview**                           | Write and call functions in any Python supported IDE. | Easily plug in parameters and run code in a prepared Docker container. | Write and call functions in RStudio. | Easily plug in parameters and run pre-written code cells in a web browser environment. |
| **Preferred programming language**     | Python                                                | Python / no preference                                                 | R                                    | Python / no preference                                                                 |
| **Recommended programming experience** | Experienced                                           | Little to none                                                         | Experienced                          | Little to none                                                                         |
| **Install dependencies?**              | Yes                                                   | No                                                                     | Yes                                  | No                                                                                     |
| **Customization flexibility**          | High                                                  | Limited                                                                | High                                 | Limited                                                                                |
| **Parameter handling**                 | Call functions                                        | Easy plug-in                                                           | Call functions                       | Easy plug-in                                                                           |
| **Run location**                       | Locally or own server                                 | Locally or own server                                                  | Locally or own server                | Remotely on AWS server                                                                 |
