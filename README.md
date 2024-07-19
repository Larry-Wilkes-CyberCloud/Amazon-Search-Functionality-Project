# Amazon Product Testing Automation with Playwright

## Overview

This project is an automated testing suite for verifying product search functionality on Amazon.com using the Playwright framework. The test scenarios include searching by product ID (ASIN), product name/text, and validating that products can be added to the shopping cart successfully. The product in focus is the "10Ft Metal Poles with Fork for Outdoor String Lights,2 Pack Light Stand for Outside Garden,Patio,Wedding,Backyard,Deck,Party."

## Test Cases

| Test Case | Objective | Results |
|-----------|-----------|---------|
| **Test Case 1: Search by ASIN** | Search for the product using its ASIN (B09L7LCZ33) and verify the correct product page is accessed. | **Passed** |
| **Test Code** | `import { test, expect } from "@playwright/test"; test("Test Case 1: Search Amazon for product with ASIN: B09L7LCZ33", async ({ page }) => { await page.goto("https://www.amazon.com/"); await page.getByPlaceholder("Search Amazon").fill("B09L7LCZ33"); await page.getByRole("button", { name: "Go" }).click(); await page.getByRole("link", { name: "10Ft Metal Poles with Fork" }).nth(1).click(); await page.getByRole("button", { name: "Add to Cart" }).click(); await page.locator("#sw-gtc").getByRole("link", { name: "Go to Cart" }).click(); });` |
| **POM Code** | `export class AmazonPage { constructor(page: Page) { this.page = page; } async navigate() { await this.page.goto("https://www.amazon.com/"); } async searchProduct(asin: string) { await this.page.getByPlaceholder("Search Amazon").fill(asin); await this.page.getByRole("button", { name: "Go" }).click(); } async selectProduct(productName: string) { await this.page.getByRole("link", { name: productName }).nth(1).click(); } async addToCart() { await this.page.getByRole("button", { name: "Add to Cart" }).click(); } async goToCart() { await this.page.locator("#sw-gtc").getByRole("link", { name: "Go to Cart" }).click(); } }` |
| &nbsp; | ![test case 1](https://github.com/user-attachments/assets/361b538a-f9e8-4c18-ae17-35ce96afc268) | &nbsp; |
| **Test Case 2: Search by Product Name/Text** | Search for the product using its descriptive name and verify the correct product page is accessed. | **Passed** |
| **Test Code** | `import { test, expect } from "@playwright/test"; test("Test Case 2: Search Amazon by product text", async ({ page }) => { await page.locator("body").click(); await page.goto("https://www.amazon.com/"); await page.getByPlaceholder("Search Amazon").fill("10Ft Metal Poles with Fork for Outdoor String Lights,2 Pack Light Stand for Outside Garden,Patio,Wedding,Backyard,Deck,Party"); await page.getByRole("button", { name: "Go" }).click(); await page.getByRole("link", { name: "Sponsored Ad - Aulimhti 10Ft" }).click(); await page.getByRole("button", { name: "Add to Cart" }).click(); });` |
| **POM Code** | `export class AmazonSearchPage { constructor(page: Page) { this.page = page; } async navigate() { await this.page.goto("https://www.amazon.com/"); } async searchProduct(productText: string) { await this.page.locator("body").click(); await this.page.getByPlaceholder("Search Amazon").fill(productText); await this.page.getByRole("button", { name: "Go" }).click(); } async selectSponsoredProduct(productName: string) { await this.page.getByRole("link", { name: productName }).click(); } async addToCart() { await this.page.getByRole("button", { name: "Add to Cart" }).click(); } }` |
| &nbsp; | ![test case 2](https://github.com/user-attachments/assets/f73d1000-ada3-4e66-8545-6323eae27d81) | &nbsp; |


