# Decentralized-Online-Marketplace-for-Sustainable-Products
Créez une place de marché en ligne décentralisée pour les produits durables, en utilisant des contrats intelligents pour garantir la transparence et la responsabilité des vendeurs.
# Simulating a Decentralized Online Marketplace for Sustainable Products

class SmartContract:
    """
    Simulates a smart contract that handles transactions and interactions
    between buyers and sellers in the marketplace.
    """
    def __init__(self):
        self.transactions = []

    def record_transaction(self, seller, buyer, product, amount):
        transaction = {
            "seller": seller.name,
            "buyer": buyer,
            "product": product.name,
            "amount": amount,
            "sustainability_rating": product.sustainability_rating
        }
        self.transactions.append(transaction)
        print(f"Transaction recorded: {transaction}")

class Product:
    """
    Represents a sustainable product listed in the marketplace.
    """
    def __init__(self, name, price, sustainability_rating):
        self.name = name
        self.price = price
        self.sustainability_rating = sustainability_rating

class Seller:
    """
    Represents a seller in the marketplace, capable of listing products.
    """
    def __init__(self, name, smart_contract):
        self.name = name
        self.products = []
        self.smart_contract = smart_contract

    def list_product(self, product):
        self.products.append(product)
        print(f"{self.name} listed a new product: {product.name}")

    def sell_product(self, buyer, product_name):
        product = next((p for p in self.products if p.name == product_name), None)
        if product:
            self.smart_contract.record_transaction(self, buyer, product, product.price)
        else:
            print("Product not found.")

class Marketplace:
    """
    Simulates the decentralized online marketplace.
    """
    def __init__(self):
        self.smart_contract = SmartContract()
        self.sellers = []

    def register_seller(self, seller_name):
        seller = Seller(seller_name, self.smart_contract)
        self.sellers.append(seller)
        print(f"Seller registered: {seller_name}")
        return seller

# Example usage
marketplace = Marketplace()

# Register sellers
seller1 = marketplace.register_seller("EcoFriendlyShop")
seller2 = marketplace.register_seller("GreenGoods")

# List products
product1 = Product("Eco Straw", 1.99, 9)
product2 = Product("Biodegradable Cup", 0.99, 8)
seller1.list_product(product1)
seller2.list_product(product2)

# Simulate a product sale
seller1.sell_product("Alice", "Eco Straw")
