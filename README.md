FScube
======

on going project

package databaseManagers;

import java.sql.Connection;
import java.sql.ResultSet;
import java.sql.SQLException;
import java.sql.Statement;

import interfaces.propertiesManager;

public class PropertiesDBManager implements propertiesManager {

  private Connection con;

	public PropertiesDBManager(Connection con) {
		this.con = con;
	}

	@Override
	public boolean addProperty(String key, String value) {

		try {
			Statement st = con.createStatement();

			String sql = " INSERT INTO Property ( prop_key, prop_value ) VALUES (" + value.getBytes() + "," + "'" + key.getBytes() + "' )";

			st.executeUpdate(sql, 1);

			ResultSet rs = st.getGeneratedKeys();

			if ( rs != null && rs.next() ){
				//???    (rs.getInt(1));
			} else {
				// TODO ERROR on adding
			}

		} catch (SQLException e) {
			// TODO
			e.printStackTrace();
		}

	}

	@Override
	public boolean updateProperty(String key, String value) {
		return false;
	}

	@Override
	public String deleteProperty(String key) {

		try{
			Statement st = con.createStatement();

			st.executeUpdate(" DELETE FROM `Property` " + 
					"WHERE `prop_key` = " + key);

		} catch (SQLException e){
			// TODO
			e.printStackTrace();
		}
		return key; 
	}

	@Override
	public String queryProperty(String prop) {

		try{
			Statement st = con.createStatement();

			st.executeQuery(" SELECT * FROM `Property` WHERE `prop_key` = " + prop);

			ResultSet rs = st.getResultSet();

			if (rs != null && rs.next()){
				// ???	return new Property(rs.getString(1));
			} else {
				return null;
			}

		} catch (SQLException e){
			// TODO TODO
			e.printStackTrace();
			return null;
		} 
	}

}
