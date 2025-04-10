# TikTokReportTool
TikTokReportTool
from selenium import webdriver
from selenium.webdriver.common.by import By
import time

def report_tiktok_user(username, reason):
    # Path to your ChromeDriver
    driver = webdriver.Chrome(executable_path='/path/to/chromedriver')  # Replace with your actual path of ChromeDriver

    # Visit the user's TikTok profile page
    url = f"https://www.tiktok.com/@{username}"
    driver.get(url)

    # Wait for the page to load
    time.sleep(5)  # Adjust the wait time based on your internet speed

    try:
        # Find and click the three dots (more options button) in the user's profile
        more_options_button = driver.find_element(By.XPATH, '//div[@data-e2e="more-options"]')
        more_options_button.click()

        # Wait for the options to appear
        time.sleep(3)

        # Click on the 'Report' button
        report_button = driver.find_element(By.XPATH, '//*[text()="Report"]')  # XPath for the Report button
        report_button.click()

        # Wait for the report options to load
        time.sleep(3)

        # Select the reason for reporting (Dropdown or direct option based on TikTok's design)
        reason_option = driver.find_element(By.XPATH, f'//*[text()="{reason}"]')  # Find the reason option
        reason_option.click()

        # Confirm the report by clicking the submit button
        submit_button = driver.find_element(By.XPATH, '//*[@data-e2e="submit-report"]')  # XPath for submit button
        submit_button.click()

        # Wait for the report to be submitted
        time.sleep(3)
        print(f"Successfully reported user @{username} for: {reason}")

    except Exception as e:
        print(f"Error occurred: {e}")

    finally:
        # Close the browser
        driver.quit()

if __name__ == "__main__":
    username = "example_user"  # Replace with the actual TikTok username
    reason = "Inappropriate content"  # Replace with the appropriate reason (e.g., "Spam", "Harassment", etc.)
    report_tiktok_user(username, reason)
