# Create a new website localy
hugo new site pingSquare-education
hugo new site kareersquare
hugo new site pingSquare-LLC
hugo new site pingsquare-Blog

# change into the directory corresponding to that website
cd pingSquare-education
cd kareersquare
cd pingSquare-LLC

# Initialize Git, hence turning "pingSquare-education" into a local repository.
git init

# Clone the "hugo-theme-relearn" theme into the themes directory, adding it to your project as a Git submodule.
git submodule add --depth 1 https://github.com/McShelby/hugo-theme-relearn.git themes/hugo-theme-relearn

# Update hugo config file hugo.toml
theme = 'hugo-theme-relearn'

# Create a homepage
hugo new --kind home _index.md

# create a new Category (Kind) that will appear like a section (chapter) and will be called "chapter"

hugo new --kind chapter Foundation/_index.md
hugo new --kind chapter CCNP-Enterprise/_index.md
    hugo new content/CCNP-Enterprise/ENCOR/_index.md
        hugo new content/CCNP-Enterprise/ENCOR/Chapter-1.md
        hugo new content/CCNP-Enterprise/ENCOR/Chapter-2.md
        hugo new content/CCNP-Enterprise/ENCOR/Chapter-3.md
        hugo new content/CCNP-Enterprise/ENCOR/Chapter-4.md
        hugo new content/CCNP-Enterprise/ENCOR/Chapter-5.md
        hugo new content/CCNP-Enterprise/ENCOR/Chapter-6.md
        hugo new content/CCNP-Enterprise/ENCOR/Chapter-7.md
        hugo new content/CCNP-Enterprise/ENCOR/Chapter-8.md
        hugo new content/CCNP-Enterprise/ENCOR/Chapter-9.md
        hugo new content/CCNP-Enterprise/ENCOR/Chapter-10.md
        hugo new content/CCNP-Enterprise/ENCOR/Chapter-11.md
        hugo new content/CCNP-Enterprise/ENCOR/Chapter-12.md
        hugo new content/CCNP-Enterprise/ENCOR/Chapter-13.md

# adding content under the chapters
hugo new basics/first-content/_index.md
hugo new basics/second-content/index.md
hugo new basics/third-content.md

# dry run of the configuration
hugo serve

# Deploy the configuration
hugo

# creating a first commit to the remote Repo
echo "# pingsquare-education" >> README.md
git init
git add README.md
git commit -m "first commit"
git branch -M main
git remote add origin https://github.com/ping-square/pingsquare-education.git
git push -u origin main

# moving the local repo to the remote repo
git add .
git commit -m "moving the local repo to the remote repo"
git push origin main 

# creating a workflow to upload to the remote repo
cp -R ../prudenceDjembat/.github/workflows/hugo.yaml . 
git add .
git commit -m "creating a workflow to upload to the remote repo"
git push origin main

# To change the variant (Website background color), paste the portion below in the main hugo.toml file
[params]
  themeVariant = 'relearn-light'

# NOTE
I noticed that when you create multiple repos under the same organization with hugo, the will appear as subfolder of your domain.
- for example my domain is ping-sqaure.com and the first and main repo attached to that domain is "ping-square.github.io". Therefore when opening ping-sqaure.com, it will show the content of "ping-square.github.io".
- If I create a second repo like "pingsquare-education", it will show under the domain as follows: https://ping-square.com/pingsquare-education/

# changing the Logo 

# Using "Arberia Theme" as the homepage of my blog

# Using "Ed" theme for the different articles in my blog

# using "aafu" theme for my portfolio

# sample frontmatter
    +++
    title = "Deploy a Hugo Powered blog to Github Pages"
    date = 2024-09-08T09:31:39-05:00
    summary = "How do you get a blog for free along with free hosting..."
    description = "This is a step-by-step tutorial that will guide the reader through the proccess of setting up a free blog with free hosting"
    draft = false
    toc = false
    readTime = true
    autonumber = false
    math = true
    tags = ["database", "java"]
    showTags = false
    hideBackToTop = false
    +++

# Sample GPT questions
25 sample comprehension questions on chapter 6 of the book 
"CCNP and CCIE Enterprise Core ENCOR 350-401 Official Cert Guide, 2nd Edition"

# sample CCNP labs
https://www.ccri.edu/faculty_staff/comp/jmowry/CCNP_Enterprise_Core_ENCOR/ENCOR_Pages/ENCOR_Page_4.htm