class Building
  attr_reader   :name,
                :address,
                :owners,
                :building_revenue

  def initialize(name, address)
    @name = name
    @address = address
    @owners = []
    @building_revenue = 0
  end

  def add_owner(owner)
    @owners << owner
  end

  def calculate_building_revenue
    @building_revenue = @owners.inject(0) do |total, owner|
      total += owner.dues
    end
  end

end
