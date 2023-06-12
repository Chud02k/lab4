# lab4
#include <iostream>
#include <string>
#include <filesystem>

namespace fs = std::filesystem;

void findSubdirectory(const std::string& directory, const std::string& subdirectoryName)
{
    for (const auto& entry : fs::directory_iterator(directory))
    {
        if (entry.is_directory() && entry.path().filename() == subdirectoryName)
        {
            std::cout << "Found subdirectory: " << entry.path() << std::endl;
        }
    }
}

void processDirectory(const std::string& directory)
{
    for (const auto& entry : fs::directory_iterator(directory))
    {
        if (entry.is_regular_file())
        {
            std::cout << "Processing file: " << entry.path() << std::endl;
            
        }
    }
}

void processFilesWithPattern(const std::string& directory, const std::string& pattern)
{
    for (const auto& entry : fs::directory_iterator(directory))
    {
        if (entry.is_regular_file() && fs::path(entry).extension() == pattern)
        {
            std::cout << "Processing file with pattern: " << entry.path() << std::endl;
            
        }
    }
}

int main(int argc, char* argv[])
{
    if (argc < 2)
    {
        std::cout << "Usage: program_name directory [subdirectory_name] [pattern]" << std::endl;
        return 1;
    }

    std::string directory = argv[1];

    if (argc == 3)
    {
        std::string subdirectoryName = argv[2];
        findSubdirectory(directory, subdirectoryName);
    }
    else if (argc == 4)
    {
        std::string pattern = argv[3];
        processFilesWithPattern(directory, pattern);
    }
    else
    {
        processDirectory(directory);
    }

    return 0;
}
