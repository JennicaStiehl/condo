class CashFlow
  attr_reader   :name,
                :cash,
                :customers,
                :month

  def initialize(name, month)
    @name = name
    @month = month
    @cash = 0
    @customers = []
  end

  def add_customer(customer)
    @customers << customer
  end

  def collect_dues
    @cash = @customers.inject(0) do |cash, customer|
      cash += customer.dues
    end
  end

end
