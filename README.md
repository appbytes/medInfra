# Medical Distribution Business Analysis

## Complete Setup and Analysis Guide

Transform hospital consumption data into actionable business intelligence for your medical distribution startup. This project provides comprehensive analysis tools including ABC classification, vendor performance evaluation, demand forecasting, and interactive HTML reports.

---

## 📋 Table of Contents

1. [Prerequisites](#prerequisites)
2. [Installation Guide](#installation-guide)
3. [Project Setup](#project-setup)
4. [Running the Analysis](#running-the-analysis)
5. [Understanding the Results](#understanding-the-results)
6. [Customization Options](#customization-options)
7. [Troubleshooting](#troubleshooting)
8. [Business Applications](#business-applications)

---

## 🎯 What This Analysis Provides

- **ABC Classification**: Identify 20% of items that drive 80% of volume
- **Vendor Consolidation Opportunities**: Find suppliers you can replace
- **Demand Forecasting**: Monthly trends and seasonal patterns
- **Category Performance**: Market size by medical category
- **Interactive Reports**: Professional HTML reports for presentations
- **Filtering Capabilities**: Focus on specific medical categories

---

## 📊 Prerequisites

### Data Requirements
- Hospital consumption data in CSV format
- Required columns: `ITEM NAME`, `QUANTITY`, `VENDOR`, `MONTH`, `YEAR`, `CATEGORY`
- Minimum 6 months of data recommended (13+ months ideal)

### System Requirements
- **Operating System**: Windows 10+, macOS 10.14+, or Linux
- **Memory**: 4GB RAM minimum (8GB recommended)
- **Storage**: 2GB free space
- **Internet**: Required for package installation

---

## 🛠 Installation Guide

### Step 1: Install R Programming Language

#### Windows:
1. Visit [https://cran.r-project.org/bin/windows/base/](https://cran.r-project.org/bin/windows/base/)
2. Click **"Download R 4.3.x for Windows"**
3. Run the downloaded `.exe` file
4. Follow installation wizard (use default settings)
5. Verify installation: Open Command Prompt, type `R --version`

#### macOS:
1. Visit [https://cran.r-project.org/bin/macosx/](https://cran.r-project.org/bin/macosx/)
2. Download the `.pkg` file for your macOS version
3. Double-click and follow installation instructions
4. Verify: Open Terminal, type `R --version`

#### Linux (Ubuntu/Debian):
```bash
sudo apt update
sudo apt install r-base r-base-dev
```

#### Using Homebrew (macOS/Linux):
```bash
brew install r
```

### Step 2: Install RStudio Desktop

#### All Platforms:
1. Visit [https://posit.co/download/rstudio-desktop/](https://posit.co/download/rstudio-desktop/)
2. Click **"Download RStudio Desktop"**
3. Select your operating system
4. Install the downloaded file
5. Launch RStudio to verify installation

#### Alternative: Using Package Managers
```bash
# macOS with Homebrew
brew install --cask rstudio

# Linux with Snap
sudo snap install rstudio --classic
```

---

## 📁 Project Setup

### Step 1: Create Project Directory
```bash
# Create project folder
mkdir medical-distribution-analysis
cd medical-distribution-analysis
```

### Step 2: Download Project Files
Create these files in your project directory:

1. **`medical_analysis_report.Rmd`** - Main R Markdown report
2. **`analysis_script.R`** - Standalone R script version
3. **`data/`** - Folder for your CSV files

### Step 3: Organize Your Data
```
medical-distribution-analysis/
├── medical_analysis_report.Rmd
├── analysis_script.R
├── data/
│   └── cleanedup_data_and_merged_and_refined.csv
├── output/
└── README.md
```

### Step 4: Open Project in RStudio

#### Method 1: RStudio Interface
1. Launch RStudio
2. **File** → **New Project** → **Existing Directory**
3. Browse to your `medical-distribution-analysis` folder
4. Click **Create Project**

#### Method 2: Command Line
```bash
# Navigate to project directory
cd medical-distribution-analysis
# Open RStudio in current directory
open -a RStudio .  # macOS
rstudio .          # Linux
```

---

## 📦 Installing Required Libraries

### Method 1: Automatic Installation (Recommended)
The R Markdown report includes automatic package installation. When you run it the first time, it will install all required packages.

### Method 2: Manual Installation
Run this code in RStudio console:

```r
# Core packages for data analysis
install.packages(c(
  "readr",          # Reading CSV files
  "dplyr",          # Data manipulation
  "ggplot2",        # Data visualization
  "plotly",         # Interactive plots
  "DT",             # Interactive tables
  "lubridate",      # Date handling
  "tidyr",          # Data reshaping
  "scales",         # Number formatting
  "knitr",          # Report generation
  "kableExtra",     # Enhanced tables
  "gridExtra",      # Multiple plots
  "viridis",        # Color schemes
  "zoo",            # Time series analysis
  "rmarkdown"       # R Markdown documents
))

# Optional packages for enhanced visualizations
install.packages(c(
  "treemapify",     # Treemap visualizations
  "forecast",       # Advanced forecasting
  "corrplot"        # Correlation plots
))
```

### Method 3: Check Installation
```r
# Verify all packages are installed
required_packages <- c("readr", "dplyr", "ggplot2", "plotly", "DT", 
                      "lubridate", "tidyr", "scales", "knitr", 
                      "kableExtra", "gridExtra", "viridis", "zoo")

missing_packages <- required_packages[!required_packages %in% installed.packages()[,"Package"]]

if(length(missing_packages) == 0) {
  print("✅ All required packages are installed!")
} else {
  print(paste("❌ Missing packages:", paste(missing_packages, collapse = ", ")))
}
```

---

## 🚀 Running the Analysis

### Step 1: Prepare Your Data
1. Place your CSV file in the `data/` folder
2. Ensure column names match: `ITEM NAME`, `QUANTITY`, `VENDOR`, `MONTH`, `YEAR`, `CATEGORY`
3. Update the file path in the R Markdown file

### Step 2: Update File Path
In `medical_analysis_report.Rmd`, find this line:
```r
data <- read_csv("cleanedup_data_and_merged_and_refined.csv")
```
Change to your file path:
```r
data <- read_csv("data/your_hospital_data.csv")
```

### Step 3: Set Category Filter (Optional)
Find this section in the R Markdown file:
```r
# SET YOUR CATEGORY FILTER HERE
selected_categories <- NULL  # All categories

# Examples:
# selected_categories <- c("Pharmaceuticals")                    # Single category
# selected_categories <- c("Pharmaceuticals", "Surgical")       # Multiple categories
```

### Step 4: Generate the Report

#### Method 1: RStudio Interface
1. Open `medical_analysis_report.Rmd` in RStudio
2. Click the **"Knit"** button
3. Wait for processing (may take 2-5 minutes)
4. HTML report will open automatically

#### Method 2: R Console
```r
# Render the report
rmarkdown::render("medical_analysis_report.Rmd")

# Specify output file name
rmarkdown::render("medical_analysis_report.Rmd", 
                  output_file = "hospital_analysis_2024.html")
```

#### Method 3: Command Line
```bash
Rscript -e "rmarkdown::render('medical_analysis_report.Rmd')"
```

---

## 📊 Understanding the Results

### Key Report Sections

#### 1. **Executive Summary**
- **KPIs**: Total units, unique products, vendors, time period
- **Filter Status**: Shows which categories are included
- **Key Findings**: High-level business opportunities

#### 2. **ABC Analysis**
- **Class A Items**: 20% of items driving 80% of volume (your focus area)
- **Class B Items**: 30% of items driving 15% of volume (standard management)
- **Class C Items**: 50% of items driving 5% of volume (minimal management)

#### 3. **Category Performance**
- Market size by medical category
- Transaction patterns
- Priority ranking for business entry

#### 4. **Vendor Analysis**
- Current supplier landscape
- Consolidation opportunities
- Market share analysis

#### 5. **Time Series Analysis**
- Monthly consumption trends
- Seasonal patterns
- Growth rates and forecasting

### Key Metrics to Focus On

| Metric | Business Importance | Action Required |
|--------|-------------------|-----------------|
| **A-Class Items** | Highest priority for inventory investment | Secure reliable suppliers |
| **High-Volume Categories** | Primary market entry targets | Develop pricing strategy |
| **Small Vendors** | Consolidation opportunities | Contact for partnerships |
| **Seasonal Trends** | Inventory planning | Adjust stock levels |

---

## 🎛 Customization Options

### Category Filtering Examples

#### High-Volume Focus
```r
selected_categories <- c("Pharmaceuticals", "Miscellaneous")
```

#### Surgical Specialization
```r
selected_categories <- c("Surgical", "Ortho", "Cardiology")
```

#### Consumables Only
```r
selected_categories <- c("General/Consumables", "Wound Care", "Respiratory")
```

#### Exclude Low-Volume Categories
```r
selected_categories <- available_categories[!available_categories %in% c("Anaesthesia", "Gastroenterology")]
```

### Report Customization

#### Change Report Theme
```yaml
output:
  html_document:
    theme: cerulean     # Options: default, cerulean, journal, flatly, readable, spacelab, united, cosmo
```

#### Create PDF Report
```yaml
output:
  pdf_document:
    toc: true
    number_sections: true
```

#### Create Dashboard Version
```r
# Install flexdashboard
install.packages("flexdashboard")

# Change output to:
output: flexdashboard::flex_dashboard
```

---

## 🔧 Troubleshooting

### Common Issues and Solutions

#### Issue: "Package not found"
```r
# Solution: Install missing packages
install.packages("package_name")
```

#### Issue: "File not found"
```r
# Check current directory
getwd()

# List files in directory
list.files()

# Set correct working directory
setwd("/path/to/your/project")
```

#### Issue: "Date parsing errors"
```r
# Check date format in your data
unique(data$MONTH)
unique(data$YEAR)

# Manual date creation if needed
data$Date <- as.Date(paste(data$YEAR, data$MONTH, "01"), format = "%Y-%B-%d")
```

#### Issue: "Memory issues with large datasets"
```r
# Increase memory limit (Windows)
memory.limit(size = 8000)

# Use data.table for large files
install.packages("data.table")
library(data.table)
data <- fread("your_file.csv")
```

#### Issue: "Knit fails with encoding errors"
```r
# Try different encoding
data <- read_csv("file.csv", locale = locale(encoding = "UTF-8"))
```

### Performance Optimization

#### For Large Datasets (10,000+ rows)
```r
# Use data.table instead of dplyr
library(data.table)
data <- fread("large_file.csv")

# Reduce figure resolution
knitr::opts_chunk$set(dpi = 150)  # Instead of default 300

# Cache results
knitr::opts_chunk$set(cache = TRUE)
```

#### Speed Up Report Generation
```r
# Disable interactive plots for faster rendering
knitr::opts_chunk$set(plotly = FALSE)

# Sample data for testing
data_sample <- data %>% sample_n(1000)
```

---

## 💼 Business Applications

### Immediate Actions (Week 1-2)

#### 1. **Identify A-Class Items**
```r
# Run ABC analysis for all categories
selected_categories <- NULL
# Focus on top 20 A-class items from report
```

#### 2. **Category Selection**
```r
# Analyze high-volume categories
selected_categories <- c("Pharmaceuticals", "Surgical")
# Compare market opportunities
```

#### 3. **Vendor Research**
```r
# Identify consolidation targets
# Look for vendors with <5% market share
# Contact for partnership discussions
```

### Medium-term Strategy (Month 1-3)

#### 1. **Inventory Planning**
- Use monthly trends for reorder points
- Calculate safety stock for A-class items
- Plan seasonal inventory adjustments

#### 2. **Pricing Strategy**
- Research wholesale prices for top items
- Analyze competitor vendor margins
- Develop pricing model by category

#### 3. **Customer Acquisition**
- Use hospital patterns to target similar facilities
- Develop value propositions by category
- Create sales materials from report insights

### Long-term Goals (3-12 months)

#### 1. **Technology Integration**
- Automate report generation
- Implement inventory management systems
- Develop customer portals

#### 2. **Market Expansion**
- Scale successful model to other regions
- Add new medical categories
- Develop specialized services

---

## 📈 Advanced Features

### Automated Report Scheduling
```r
# Install required packages
install.packages(c("taskscheduleR", "cronR"))

# Schedule weekly reports
library(taskscheduleR)
taskscheduler_create(
  taskname = "medical_analysis", 
  rscript = "medical_analysis_report.Rmd",
  schedule = "WEEKLY"
)
```

### Email Integration
```r
# Install email packages
install.packages(c("blastula", "gmailr"))

# Send reports via email
library(blastula)
email <- render_email("medical_analysis_report.Rmd")
smtp_send(email, to = "stakeholder@company.com")
```

### Database Integration
```r
# Connect to databases
install.packages(c("DBI", "RMySQL", "RPostgreSQL"))

# Example: Connect to MySQL
library(DBI)
con <- dbConnect(RMySQL::MySQL(), 
                 dbname = "hospital_data",
                 host = "localhost", 
                 user = "username", 
                 password = "password")

data <- dbGetQuery(con, "SELECT * FROM consumption_data")
```

---

## 🤝 Support and Resources

### Documentation
- [R Documentation](https://www.r-project.org/help.html)
- [RStudio Guides](https://support.rstudio.com/hc/en-us)
- [R Markdown Reference](https://rmarkdown.rstudio.com/)

### Community Support
- [R Community](https://community.rstudio.com/)
- [Stack Overflow R Tag](https://stackoverflow.com/questions/tagged/r)
- [Reddit r/rstats](https://www.reddit.com/r/rstats/)

### Getting Help
1. Check the troubleshooting section above
2. Search error messages on Stack Overflow
3. Post questions with reproducible examples
4. Include session info: `sessionInfo()`

---

## 📝 Project Structure Reference

```
medical-distribution-analysis/
├── README.md                              # This guide
├── medical_analysis_report.Rmd            # Main R Markdown report
├── analysis_script.R                      # Standalone R script
├── data/
│   ├── cleanedup_data_and_merged_and_refined.csv
│   └── hospital_data_backup.csv
├── output/
│   ├── medical_analysis_report.html      # Generated HTML report
│   ├── abc_analysis_results.csv          # ABC classification export
│   ├── category_performance.csv          # Category analysis export
│   ├── vendor_performance.csv            # Vendor analysis export
│   └── monthly_trends.csv                # Time series export
├── figures/                               # Generated plots
└── cache/                                 # Cached computations
```

---

## 🔄 Version History

- **v1.0** - Initial release with basic ABC analysis
- **v1.1** - Added category filtering capabilities
- **v1.2** - Enhanced interactive tables and visualizations
- **v1.3** - Added business recommendations and action items

---

## 📄 License

This project is provided as-is for business analysis purposes. Feel free to modify and adapt for your specific needs.

---

## 🎯 Quick Start Checklist

- [ ] Install R programming language
- [ ] Install RStudio Desktop
- [ ] Create project directory
- [ ] Place CSV data file in correct location
- [ ] Update file path in R Markdown
- [ ] Install required packages
- [ ] Set category filter (optional)
- [ ] Generate HTML report
- [ ] Review ABC analysis results
- [ ] Identify top business opportunities

**Ready to transform your hospital data into business intelligence? Start with Step 1 above! 🚀**
