class Owner
    attr_reader   :name,
                  :unit,
                  :building,
                  :dues

  def initialize(attributes)
    @name = attributes[:name]
    @unit = attributes[:unit]
    @building = attributes[:building]
    @dues = attributes[:dues]
  end
end
