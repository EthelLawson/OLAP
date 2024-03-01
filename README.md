class SalesData:
    def __init__(self, product, region, date, amount):
        self.product = product
        self.region = region
        self.date = date
        self.amount = amount


class OLAPModel:
    def __init__(self):
        self.sales_data = []

    def add_sales_data(self, sales_data):
        self.sales_data.append(sales_data)

    def get_sales_data(self):
        return self.sales_data


class OLAPProcessor:
    def __init__(self, olap_model):
        self.olap_model = olap_model

    def total_sales_by_region(self):
        sales_data = self.olap_model.get_sales_data()
        result = {}
        for data in sales_data:
            if data.region not in result:
                result[data.region] = 0
            result[data.region] += data.amount
        return result

    def total_sales_by_product(self):
        sales_data = self.olap_model.get_sales_data()
        result = {}
        for data in sales_data:
            if data.product not in result:
                result[data.product] = 0
            result[data.product] += data.amount
        return result


# 示例用法
olap_model = OLAPModel()
olap_model.add_sales_data(SalesData("Product A", "Region 1", "2023-01-01", 100))
olap_model.add_sales_data(SalesData("Product B", "Region 2", "2023-01-02", 150))
olap_model.add_sales_data(SalesData("Product A", "Region 1", "2023-01-03", 200))

olap_processor = OLAPProcessor(olap_model)
total_sales_by_region = olap_processor.total_sales_by_region()
total_sales_by_product = olap_processor.total_sales_by_product()

print("Total Sales by Region:")
print(total_sales_by_region)
print("Total Sales by Product:")
print(total_sales_by_product)
