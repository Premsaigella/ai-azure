# AI Project: Smart Document Reader



import cv2
import pytesseract
from azure.ai.vision import VisionServiceClient
from azure.identity import DefaultAzureCredential


endpoint = "YOUR_AZURE_ENDPOINT"
credential = DefaultAzureCredential()
vision_client = VisionServiceClient(endpoint, credential)

def extract_text(image_path):
    """Extracts text from an image using Azure AI Vision OCR."""
    image = open(image_path, "rb")
    response = vision_client.extract_text(image)
    return response.text

def read_text(image_path):
    """Process the image using OpenCV and Tesseract OCR"""
    img = cv2.imread(image_path)
    gray = cv2.cvtColor(img, cv2.COLOR_BGR2GRAY)
    text = pytesseract.image_to_string(gray)
    return text


image_path = "sample_document.jpg"
azure_text = extract_text(image_path)
local_ocr_text = read_text(image_path)

print("Extracted Text using Azure AI Vision:", azure_text)
print("Extracted Text using Local OCR:", local_ocr_text)
