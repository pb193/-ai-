Below is a bilingual README (Chinese and English) for your Python script, a folder analysis and cleanup tool. It includes an overview, features, requirements, installation instructions, usage guide, and additional notes.

文件夹归属分析与清理工具 / Folder Attribution Analysis and Cleanup Tool
概述 / Overview
中文
这是一个基于 Python 的图形界面应用程序，旨在扫描、分析和清理 Windows 系统上的文件夹。它利用人工智能（通过阿里云 DashScope API 调用）、注册表数据和本地启发式方法来判断文件夹的所有者、用途以及删除的影响。该工具提供了一个基于 tkinter 的用户友好界面，用于显示文件夹详情、优先级排序并安全地将不需要的文件夹移至回收站。

该应用程序特别适用于识别残留或不必要的文件夹，同时保护关键系统目录。它支持缓存以加速后续扫描，并集成了模糊匹配以提高文件夹识别率。

当前版本: 1.0

最后更新: 2025年3月27日

English
This is a Python-based GUI application designed to scan, analyze, and clean up folders on a Windows system. It leverages AI (via an API call to Aliyun DashScope), registry data, and local heuristics to determine the ownership, purpose, and impact of deleting folders. The tool provides a user-friendly interface built with tkinter to display folder details, prioritize cleanup, and safely move unwanted folders to the recycle bin.

The application is particularly useful for identifying residual or unnecessary folders while protecting critical system directories. It supports caching for faster subsequent scans and integrates fuzzy matching for improved folder recognition.

Current Version: 1.0

Last Updated: March 27, 2025

功能 / Features
中文
文件夹扫描: 扫描指定路径的第一层子目录。
AI 驱动分析: 使用 API（阿里云 DashScope）推断文件夹的所有者、应用程序和用途，并附带置信度评分。
注册表集成: 从 Windows 注册表中交叉引用已安装应用程序以确保归属准确性。
模糊匹配: 使用 fuzzywuzzy 对已知文件夹列表进行稳健的名称匹配。
缓存: 将分析结果存储在 JSON 文件（folder_cache.json）中，以加速后续扫描。
安全特性:
保护关键系统文件夹（如 "Windows"、"Program Files"）。
使用 psutil 检查文件是否在使用中以避免删除。
通过 send2trash 将删除项移至回收站，而非永久删除。
图形界面:
在表格中显示文件夹详情（路径、归属、影响、优先级、大小）。
支持手动选择或基于优先级的批量选择/删除。
为详细归属信息提供工具提示。
异步处理: 使用 asyncio 和 aiohttp 实现高效的 API 调用和文件夹分析。
English
Folder Scanning: Scans the first-level subdirectories of a specified path.
AI-Powered Analysis: Uses an API (Aliyun DashScope) to infer folder ownership, application, and purpose with confidence scores.
Registry Integration: Cross-references installed applications from the Windows registry for accurate attribution.
Fuzzy Matching: Employs fuzzywuzzy for robust folder name matching against a known list.
Caching: Stores analysis results in a JSON file (folder_cache.json) to speed up future scans.
Safety Features:
Protects critical system folders (e.g., "Windows", "Program Files").
Checks if files are in use before deletion using psutil.
Moves deleted items to the recycle bin via send2trash instead of permanent deletion.
GUI Interface:
Displays folder details (path, ownership, impact, priority, size) in a table.
Allows manual selection or priority-based batch selection/deletion.
Provides tooltips for detailed ownership info.
Asynchronous Processing: Uses asyncio and aiohttp for efficient API calls and folder analysis.
要求 / Requirements
中文
操作系统: Windows（由于需要访问注册表和使用 send2trash）。
Python 版本: Python 3.8 或更高版本。
依赖项:
tkinter（通常随 Python 附带；如缺失需安装 python-tk）
aiohttp（用于异步 HTTP 请求）
psutil（用于进程和文件使用检查）
send2trash（用于安全删除至回收站）
fuzzywuzzy（用于模糊字符串匹配）
python-Levenshtein（可选，加速 fuzzywuzzy）
pathlib（Python 标准库中包含）
winreg（Python 标准库中包含，仅限 Windows）
English
Operating System: Windows (due to registry access and send2trash usage).
Python Version: Python 3.8 or higher.
Dependencies:
tkinter (usually included with Python; install python-tk if missing)
aiohttp (for asynchronous HTTP requests)
psutil (for process and file usage checks)
send2trash (for safe deletion to recycle bin)
fuzzywuzzy (for fuzzy string matching)
python-Levenshtein (optional, speeds up fuzzywuzzy)
pathlib (included in Python standard library)
winreg (included in Python standard library, Windows only)
安装 / Installation
中文
安装 Python: 确保已安装 Python 3.8 或更高版本（下载地址)。
克隆或下载代码: 将此项目保存到本地。
安装依赖:
bash


pip install aiohttp psutil send2trash fuzzywuzzy python-Levenshtein
配置 API: 在代码中将 headers = {"Authorization": ""} 修改为您的阿里云 DashScope API 密钥。
运行程序:
bash

python cleaner_app.py
English
Install Python: Ensure Python 3.8 or higher is installed (download here).
Clone or Download Code: Save this project to your local machine.
Install Dependencies:
bash



pip install aiohttp psutil send2trash fuzzywuzzy python-Levenshtein
Configure API: Replace headers = {"Authorization": ""} in the code with your Aliyun DashScope API key.
Run the Program:
bash



python cleaner_app.py
使用指南 / Usage Guide
中文
启动程序: 运行脚本后，图形界面将显示。
选择路径: 点击“选择文件夹”按钮，选择要扫描的目录。
开始扫描: 点击“开始 AI 扫描”按钮，程序将分析第一层子文件夹。
查看结果: 扫描完成后，表格将显示文件夹路径、归属、删除影响、优先级和大小。
选择与删除:
手动勾选文件夹并点击“删除选中项（移至回收站）”。
点击“根据建议选择”自动勾选高优先级文件夹。
点击“根据建议批量删除”直接删除高优先级文件夹。
停止扫描: 如需中断，点击“停止扫描”按钮。
缓存管理: 程序自动保存和加载缓存（folder_cache.json），无需手动管理。
English
Launch the Program: Run the script to open the GUI.
Select Path: Click the “Select Folder” button to choose a directory to scan.
Start Scanning: Click “Start AI Scan” to analyze the first-level subfolders.
View Results: After scanning, the table displays folder paths, ownership, deletion impact, priority, and size.
Select and Delete:
Manually check folders and click “Delete Selected (Move to Recycle Bin)”.
Click “Select by Priority” to auto-select high-priority folders.
Click “Delete by Priority” to directly delete high-priority folders.
Stop Scanning: Click “Stop Scan” to interrupt the process if needed.
Cache Management: The program automatically saves and loads the cache (folder_cache.json), no manual action required.
注意事项 / Additional Notes
中文
API 配置: 未配置有效的 API 密钥将导致 AI 分析失败，程序将依赖本地规则和注册表。
权限: 扫描系统目录（如 C:\）可能需要管理员权限。
安全性: 删除前请仔细检查高影响文件夹，以免误删重要数据。
性能: 首次扫描可能较慢，后续因缓存会显著加快。
English
API Configuration: Without a valid API key, AI analysis will fail, and the program will rely on local rules and registry data.
Permissions: Scanning system directories (e.g., C:) may require administrator privileges.
Safety: Review high-impact folders carefully before deletion to avoid losing important data.
Performance: The first scan may be slow; subsequent scans are faster due to caching.
